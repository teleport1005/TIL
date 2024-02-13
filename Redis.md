# Redis
- 일종의 데이터베이스 구조(데이터를 모아두는 공간)
- 영속성 데이터가 아니며 디스크가 아닌 RAM 메모리에 데이터를 저장

> 일반적인 관계형 데이터베이스?  
> 서버의 형태로 가동되어 파일 시스템에 데이터를 저장  
> 데이터에 영속성을 부여하나 읽고 쓰는 시간이 비교적 길다  
>✏ 상황에 따라 일시적인 In-Memory 데이터베이스가 필요할 수 있다  
>✏ 임시 데이터, 자주 읽혀야 하는 데이터 등..

## Redis란?
- REmote DIctionary Server(DIctionary: 자료 구조)
- Key-Value의 형태로 데이터를 저장할 수 있게 해 주는 In-Memory Database
- 여러 어플리케이션 인스턴스에서 세션 정보 공유(여러 어플리케이션에서 접근이 가능)
- 관계형 데이터베이스의 데이터를 임시로 저장하는 캐시

### Key - Value 자료 구조
- String, List, Set, Hash, Sorted Set 제공
- 잘못된 자료형의 명령을 전달하면 오류가 발생하나 `Key`가 없어도 동작은 한다
- `Key`에 특정 자료형의 데이터(`Value`)를 넣은 후, `key`를 가지고 회수하는 방식

###  String

- 가장 기본이 되는 자료형
- `SET`, `GET`을 사용하여 저장과 회수가 가능
```
-- SET key value, GET key
SET string "string value"
GET string
```

- 문자열로 저장된 정수형 데이트는 값의 증감 가능
```
SET intstring 1
INCR intstring // 정수 데이터 1 증가
DECR intstring // 정수 데이터 1 감소
```

- 여러 데이터를 한번에 저장하거나 가져올 수 있음
```
MSET name ami age 25 married false
MGET name age married
```

### List
- 여러 문자열 데이터를 Linked List 형태로 저장
- List의 앞과 뒤에서 데이터를 저장하거나 가져올 수 있음(Stack, Queue로 사용)
```
LPUSH fruitlist apple -- [apple]
RPUSH fruitlist banana -- [apple, banana]
LPUSH fruitlist coconut -- [coconut, apple, banana]
RPUSH fruitlist durian -- [coconut, apple, banana, durian]
```
```
RPOP fruitlist -- [durian]
LPOP fruitlist -- [coconut]

LLEN fruitlist -- 저장된 리스트의 길이를 반환
LRANGE fruitlist 0 4 -- 0부터 4(start부터 end)까지의 원소들을 반환
```

### SET
- 문자열의 집합(중복 없음, 순서 없음, 집합 연산 가능)
```
-- SET
SADD students alex -- value 추가
```
```
SMEMBERS students -- 집합의 모든 원소 반환
SISMEMBER students alex -- 해당 value가 존재하는지 반환

SREM students alex -- 해당 value를 제거
SCARD students -- 집합의 길이 반환
```

### Hash
- Field와 Value로 이루어진 자료 구조
- 특정 `key`에 hash를 만들어 내부 field를 정의하고 value를 저장할 수 있음
- Map<String, Map<String, String>>
```
HSET alexinfo name alex age 20 -- key의 Hash에 field에 value를 저장
HSET alexinfo major CSE -- 한 번에 여러 쌍 저장 가능
HSET alexinfo name "alex rodriguez"
```
```
HGET alexinfo name -- 저장된 value 반환 (없으면 null)
HGET alexinfo age

HMGET alexinfo name age major -- key에 저장된 Hash에서 복수의 field에 저장된 value 반환

HGETALL alexinfo -- field - value를 전부 반환
HKEYS alexinfo --  저장된 field를 전부 반환
HVALS alexinfo --  저장된 value를 전부 반환
HLEN alexinfo -- 저장된 field의 갯수를 반환
```

### Sorted Set
- 정렬 집합(중복 없음)
- 데이터의 score를 저장하여 최소, 최대를 구하기 용이
```
-- Sorted Set
ZADD grades 10 alex
ZADD grades 9 brad 11 chad -- score를 점수로 가진 member를 추가
ZADD grades 8 alex --  이미 있는 member의 경우 새로운 score를 설정
```
```
ZINCRBY grades 1 alex -- member의 score를 increment 만큼 증가(음수로 감소시킬 수 있음)

ZRANK grades alex --  member의 순위를 오름차순 기준으로 0에서부터 계산하여 반환
ZRANGE grades 0 3 -- start 부터 stop 순위까지 오름차순 기준으로 반환
```

### EXPIRE
- 특정 `key`의 만료 시간을 초 단위로 지정 가능
```
SET expirekey "to be expired"
EXPIRE expirekey 20 -- 20sec 뒤에 만료
GET expirekey
```

### DEL
- `key` 제거
```
DEL grades
DEL students
```

### FLUSHDB
- 전체의 `key` 제거
```
FLUSHDB
```
