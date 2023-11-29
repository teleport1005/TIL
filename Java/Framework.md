## Collections Framework
- Generic을 활용해 다수의 데이터 관리하기
- Java에서 만들어 놓은 데이터 정리용 클래스
- `interface`를 활용하여 사용 방식 통일 후 구현하는 도구 모음

### Set
- = 집합 / 원소 선별 용도로 사용
- 중복 허용하지 않음
- 순서 개념 없음
```Java
 Set<String> skillSet = new HashSet<>();
        skillSet.add("md");
        skillSet.add("git");
        skillSet.add("java"); // 중복 데이터 추가 불가
        skillSet.add("oop");
        skillSet.add("java");
```
```Java
System.out.println(skillSet); 
-> [oop, git, java, md] // 데이터 순서 보장 불가
```
1. `교집합` 연산 가능
```Java
System.out.println(skillSet.addAll(skillList));
```
>`skillList`에서 없는 `skillSet`에 없는 원소들만 선별하여 추가함  
> 추가 성공 여부 `boolean` 값으로 반환함

### List
- 순서를 가짐
- 중복 허용
- 추가, 제거, 특정 위치의 원소 가져오기 가능
```Java
 List<String> names = new ArrayList<>();
        names.add("Alex");  
        names.add("Brad");  
        names.add("Dave");  
        names.add("Eric");
```
1. 특정 위치의 데이터 확인 가능
```Java
System.out.println(names.get(2));
```
2. 중간에 새로운 데이터 추가 가능
```Java
names.add(2, "Chad");
```
3. 데이터의 위치 찾기 가능
```Java
System.out.println(
  "Chad is at: " + names.indexOf("Chad"));
```
4. 데이터 제거 가능
```Java
System.out.println(names.remove(3));// 순서를 기준으로
System.out.println(names.remove("Eric")); // 값을 기준으로
```
>제거 성공 여부는 `boolean` 값으로 반환된다

### Map
- `Key`와 `Value`의 쌍으로 이루어진 인터페이스
- 데이터와 그 데이터를 찾기 위한 `key`를 함께 저장함
- `Key`는 중복 불가, 값은 중복 가능
```Java
   Map<String, String> contactBook = new HashMap<>();
        contactBook.put("Alex", "010-1234-1234");
        contactBook.put("Brad", "010-2222-2222");
        contactBook.put("Chad", "010-3333-3333");
        contactBook.put("Dave", "010-4444-4444");
```
>`Key` = 이름, `Value` = 연락처 `Map` = 전화번호부

1. `Key`를 사용하여 `Value` 가져오기
```Java
System.out.println(contactBook.get("Alex"));
System.out.println(contactBook.get("Ami"));
---
010-1234-1234 // KEY "Alex"의 값 확인
null // KEY "Ami"는 없기 때문에 null 값 확인
```
2. 데이터 추가하기
```java
contactBook.put("Ami", "010-5555-5555");
// 새로운 Key값 추가
contactBook.put("Alex", "010-1111-1111");
// 기존에 있는 Key를 추가하면 값이 덮어씌워짐
System.out.println(contactBook);
---
{Alex=010-1111-1111, Chad=010-3333-3333, Brad=010-2222-2222, Dave=010-4444-4444, Ami=010-5555-5555}
```