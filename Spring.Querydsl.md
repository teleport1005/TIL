## Query dsl Basics
- dsl: domain specific language 
- Query dsl은 DB 데이터를 참조하기 위한 목적으로 사용하는 언어
- Java 코드로 데이터를 조회하는 것이 목표


---

### And & Or
- And와 Or를 사용하는 방법을 알아보자
- 기본적으로 Where절에 복수 개를 입력하면 and로 간주한다
```Java
    public void andOr() {
        List<Item> foundItems = queryFactory
                .selectFrom(item)
                .fetch();

        for (Item found: foundItems) {
            System.out.println(found);
        }
```
```
Item{id=1, name='itemA', description='null', price=5000, stock=20} 
Item{id=2, name='itemB', description='null', price=6000, stock=30} 
Item{id=3, name='itemC', description='null', price=8000, stock=40} 
Item{id=4, name='itemD', description='null', price=10000, stock=50} 
Item{id=5, name='itemE', description='null', price=5500, stock=10} 
Item{id=6, name='null', description='null', price=7500, stock=25} 
```
#### 연습하기 
```Java
foundItems = queryFactory
        .selectFrom(item)
        // 가격이 6000 이하 또는 9000 이상
        // .and() 또는 .or()를 연쇄 호출할 수 있다 (method chaining)
        .where(
                // ]{item.price <= 6000
                item.price.loe(6000)
                        // OR (item.price >= 9000)}
                        .or(item.price.goe(9000))
                        // OR (item.stock in (20, 30, 40)]
                        .or(item.stock.in(20, 30, 40))
                        // AND item.name is not null
                        .and(item.name.isNotNull())
        )
```
- 가격이 6,000원 이하 또는 9,000원 이상 제품이면서 재고가 40 미만 또는 60 초과되는 제품 조회

```Java
.where(
        item.price.loe(6000).or(item.price.goe(9000)),
        item.stock.lt(40).or(item.stock.gt(60))
 )
```
- 여러가지 조건을 묶어 하나의 조건으로 만들어 줄 수 있다

### Join
- `.join`으로 사용 가능
- Left, RIGHT 모두 사용 가능
```Java
    @Test
    public void regularJoins() {
        List<Item> foundList = queryFactory
                .selectFrom(item)
                .join(item.shop)
                .fetch();

        for (Item found: foundList) {
            System.out.println(found);
        }
    }
```
```
Item{id=1, name='itemA', description='null', price=5000, stock=20} 
Item{id=2, name='itemB', description='null', price=6000, stock=30} 
Item{id=3, name='itemC', description='null', price=8000, stock=40} 
Item{id=4, name='itemD', description='null', price=10000, stock=50} 
```
- `Fetch Join` 사용
```Java
    @Autowired
    private EntityManager entityManager;

    @Test
    public void fetchJoin() {
        // 영속성 컨텍스트 초기화
        entityManager.flush();
        entityManager.clear();

        // 그냥 join은 연관 데이터를 불러오지는 않는다
        Item found = queryFactory
                .selectFrom(item)
                .join(item.shop)
                .where(item.name.eq("itemA"))
                .fetchOne();
        assertFalse(unitUtil.isLoaded(found.getShop()));

        found = queryFactory
                .selectFrom(item)
                .join(item.shop)
                // Fetch Join으로 변경
                .fetchJoin()
                .where(item.name.eq("itemB"))
                .fetchOne();
        assertTrue(unitUtil.isLoaded(found.getShop()));
    }

```
- 집계 함수 `aggregate` 사용
```Java
    @Test
    public void aggregate() {
        // Querydsl의 Tuple
        Tuple result = queryFactory
                // 집계하고 싶은 속성의 집계함수 메서드를 호출하여 select에 추가
                // item.(속성).(집계함수)()
                .select(
                        item.count(),
                        item.price.avg(),
                        item.price.max(),
                        item.stock.sum()
                )
                .from(item)
                .fetchOne();
        // Tuple은 조회했던 QType의 속성 및 집계를 기준으로 데이터 회수 가능
        assertEquals(6, result.get(item.count()));
        assertEquals(175, result.get(item.stock.sum()));
        // 없는 건 null로 반환
        System.out.println(result.get(item.stock));

        List<Tuple> results = queryFactory
                .select(
                        shop.name,
                        item.count(),
                        item.price.avg(),
                        item.stock.sum()
                )
                .from(item)
                .join(item.shop)
                .groupBy(shop.name)
                .fetch();

        for (Tuple tuple: results) {
            System.out.printf(
                    "%s: %d, %.2f (%d)%n",
                    tuple.get(shop.name),
                    tuple.get(item.count()),
                    tuple.get(item.price.avg()),
                    tuple.get(item.stock.sum())
            );
        }
    }
```


## Querydsl Extra
 ### Projection
  - 속성들을 결합하여 따로 조회하고 싶다면 `Tuple` 사용
  - 단일 결과라면 자료형으로 반환
```Java
    @Test
    public void noProjection() {
        // 하나의 속성을 조회할 때는, 해당 속성의 자료형으로 반환된다
        String name = queryFactory
                .select(item.name)
                .from(item)
                .where(item.id.eq(4L))
                .fetchOne();
        assertEquals("itemD", name);

        // 집계함수 활용 가능
        Long count = queryFactory
                .select(item.count())
                .from(item)
                .fetchOne();
        assertEquals(6L, count);

        // fetch는 List로
        List<String> names = queryFactory
                .select(item.name)
                .from(item)
                .fetch();
        for (String foundName: names) {
            System.out.println(foundName);
        }

        // 단일 속성이 아니면 Tuple
        Tuple resultTuple = queryFactory
                .select(item.price, item.stock)
                .from(item)
                .where(item.name.eq("itemB"))
                .fetchOne();
        assertEquals(6000, resultTuple.get(item.price));
        assertEquals(30, resultTuple.get(item.stock));
        assertNull(resultTuple.get(item.name));

        List<Tuple> tuples = queryFactory
                .select(item.price, item.stock)
                .from(item)
                .fetch();
        for (Tuple tuple: tuples) {
            System.out.printf("%d (%d)%n", tuple.get(item.price), tuple.get(item.stock));
        }
    }
```
- dto의 형태로 데이터를 표기하는 방식
 1. Projections.bean
```Java
        // Projections.bean: Setter 기반 Projection
        itemDtoList = queryFactory
                .select(Projections.bean(
                        ItemDto.class,
                        item.name,
                        item.price,
                        item.stock
                ))
                .from(item)
                .where(item.name.isNotNull())
                .fetch();
        itemDtoList.forEach(System.out::println);
```
- `Setter`가 필요함
 2. Projections.fields
 ```Java
         // Projections.fields: 속성 기반 Projection
        itemDtoList = queryFactory
                .select(Projections.fields(
                        ItemDto.class,
                        item.name,
                        item.price,
                        item.stock
                ))
                .from(item)
                .where(item.name.isNotNull())
                .fetch();
        itemDtoList.forEach(System.out::println);
 ```
 - `Setter`를 사용하지 못하는 상황에서 활용 가능
  3. Projections.constructor
  ```Java
          // Projections.constructor: 생성자 기반 Projection
          itemDtoList = queryFactory
                .select(Projections.constructor(
                        ItemDto.class,
                        item.name,
                        item.price,
                        item.stock  
                ))
                .from(item)
                .where(
                        item.price.isNotNull(),
                        item.stock.isNotNull()
                )
                .fetch();
        itemDtoList.forEach(System.out::println);
  ```
 - 생성자를 호출할 수 있음

  4. `@QueryProjection` 
 ```Java
 public class ItemDtoProj {
    private String name;
    private Integer price;
    private Integer stock;

    @QueryProjection
    // QDto를 만들고 그 생성자를 사용하여
    // 데이터를 Projection할 수 있다.
    public ItemDtoProj(
            String name,
            Integer price,
            Integer stock
    ) {
        this.name = name;
        this.price = price;
        this.stock = stock;
    }
 ```
 ```Java
     @Test
    public void queryProjection() {
        List<ItemDtoProj> itemDtoProjList = queryFactory
                .select(new QItemDtoProj(
                        item.name,
                        item.price,
                        item.stock
                ))
                .from(item)
                .fetch();

        itemDtoProjList.forEach(System.out::println);
    }

 ```

### Dynamic Query (동적 쿼리)
- 높은 타입 안정성을 바탕으로 작성 가능
 1. `BooleanBuilder`
```Java
@Test
    public void dynamicQueryTester() {
        List<Item> results = null;
        String name = "itemA";
        Integer price = 5000;
        Integer stock = 20;

        results = booleanBuilder(name, price, stock);
        results.forEach(System.out::println);
    }

    public List<Item> booleanBuilder(
            String name,
            Integer price,
            Integer stock
    ) {
        // 1. BooleanBuilder: 여러 조건을 엮어서 하나의 조건으로 만들어진
        //                    BooleanBuilder를 사용하는 방법
        //                    생성자에 초기 조건 상정 가능
        BooleanBuilder booleanBuilder = new BooleanBuilder(item.name.isNotNull());
        // 여태까지 누적된 조건에 대하여, 주어진 조건을 AND로 엮는다.
        if (name != null)
            // (여태까지의 조건) AND i.name = name
            booleanBuilder.and(item.name.eq(name));
        if (price != null)
        // (여태까지의 조건) AND i.price = price
        booleanBuilder.and(item.price.eq(price));
        if (stock != null)
        // (여태까지의 조건) AND i.stock = stock
        booleanBuilder.and(item.stock.eq(stock));
        // i.name = name AND i.price = price AND i.stock = stock
        return queryFactory
                .selectFrom(item)
                .where(booleanBuilder)
                .fetch();
    }
```

### With Spring Data JPA
- Spring Data JPA는 커스텀 기능 구현이 가능
- 기능 통합을 하여 사용
- JpaRepository는 일종의 인터페이스
- 커스텀 기능 인터페이스를 만들어 다중 상속을 활용
```Java
public interface ItemQuerydslRepo {
    List<Item> searchDynamic(ItemSearchParams searchParams);
    Page<Item> searchDynamic(ItemSearchParams searchParams, Pageable pageable);
}
```
- ItemQuerydslRepo 인터페이스에 구현 기능 추가
```Java
public interface ItemRepository extends JpaRepository<Item, Long>, ItemQuerydslRepo {
}
```
- 다중 상속 
```Java
public class ItemQuerydslRepoImpl implements ItemQuerydslRepo {
    private final JPAQueryFactory queryFactory;
    @Override
    public List<Item> searchDynamic(ItemSearchParams searchParams) {
        return queryFactory.selectFrom(item).fetch();
    }
    @Override
    public Page<Item> searchDynamic(ItemSearchParams searchParams, Pageable pageable) {
        List<Item> content = queryFactory
                .selectFrom(item)
                .offset(pageable.getOffset())
                .limit(pageable.getPageSize())
                .fetch();
        JPAQuery<Long> countQuery = queryFactory
                .select(item.count())
                .from(item);

        return PageableExecutionUtils.getPage(content, pageable, countQuery::fetchOne);
```
- 구현 클래스 (List와 Page 구현)

