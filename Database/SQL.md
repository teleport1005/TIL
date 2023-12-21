## SQL - Structured Query Language
- 관계형 데이터베이스에서 데이터를 관리하기 위해 사용하는 언어
1. `DDL` – Data Definition Language  
  데이터의 모습을 정의하기 위한 명령
2. `DML` – Data Manipulation Language  
  데이터 조작을 위한 명령
3. `DCL` – Data Control Language  
  데이터 접근 권한 관련 

  ### SQL 기본 문법
  - `SELECT`, `INSERT` 등의 키워드로 시작
  ```SQL
  SELECT column_name FROM table_name;
  ```

`Statement(문)`  
  - 독립적으로 실행할 수 있는 완전한 코드조각  

`Clause(절)`
  - Statement(문)을 이루는 작은 단위

    ### CREATE TABLE 
    - 데이터베이스에 새 테이블을 만들 때 사용
    - 테이블 이름을 명시하고 각 필드릐 형태를 정의한다.
      ```sql
      CREATE TABLE lecturer (
        id INTEGER,
        name VARCHAR(64),
        major VARCHAR(64),
        grade VARCHAR(64),
        articles INTEGER
      );
      ```
      >`VARCHAR`는 호환성을 위해 다른 데이터베이스에서 흔하게 사용하는 타입이다.  
      >SQLite는 이러한 타입들을 변환하여 차용한다.

    컬럼 타입: SQLite 기준으로 정리
    1. NULL – 정보가 없는 데이터
    2. INTEGER – 정수형 데이터
    3. REAL – 실수형 데이터
    4. TEXT – 문자형 데이터
    5. BLOB - Binary Large Object

### 데이터 무결성과 Table Constraints
- `데이터 무결성`: 데이터가 전송, 저장되고 처리되는 모든 과정에서  변경되거나 손상되지 않고 완전성, 정확성, 일관성을 유지함을 보장하는 특성을 말한다.  
-`Table Constraints`: 데이터 무결성을 유지하기 위헤 테이블의 컬럼에 들어올 수 있는 데이터를 제한시키는 것, 또는 그의 제약 조건  
  1. NOT NULL: 컬럼에 NULL이 들어오지 못함 / 빈값 저장 불가
    ```sql
    first_name VARCHAR(64) NOT NULL,
    ```
  2. UNIQUE: 해당 컬럼의 값은 고유해야 함을 제약 / 중복 불가
    ```sql
      email VARCHAR(64) UNIQUE, 
    ```
  3. PRIMARY KEY: 해당 컬럼을 PK로 지정
    ```sql
      id INTEGER PRIMARY KEY, -- // 묵시적으로 NOT NULL이 적용된다
    ```
  4. AUTOINCREMENT: 사용되지 않은 값이나 이전의 삭제된 행의 값을 재사용하지 않는다.
    ```sql
      id INTEGER PRIMARY KEY AUTOINCREMENT, 
    ```
  > 컬럼 타입 뒤에 붙여서 사용한다


  ### ALTER TABLE  
  이미 존재하는 테이블을 수정함
  - RENAME TO: 테이블 이름을 수정  
  ```sql
  --TABLE 이름 바꾸기 
  ALTER TABLE student RENAME TO student_backup; 
  ALTER TABLE student_backup RENAME TO student;
  ```
  - RENAME COLUMN: 테이블에 칼럼이름을 변경  
  ```sql
  -- 컬럼의 이름 바꾸기 
  ALTER TABLE student RENAME COLUMN first_name TO given_name;
  ALTER TABLE student RENAME COLUMN given_name TO first_name;
  ```
  - ADD COLUMN: 테이블에 칼럼을 추가
  ```sql
  -- 컬럼 추가하기
  ALTER TABLE student ADD COLUMN address VARCHAR(256);
  ```
  ```sql
  -- 제약사항 넣어서 추가하기
  ALTER TABLE student ADD COLUMN phone VARCHAR(128) NOT NULL DEFAULT '';
  ```
    >ADD COLUMN시 제약사항을 추가할 경우, NOT NULL에 주의!  
    >이전에 생성된 데이터를 어떻게 처리할지를 결정해 주어야 함 (DEFAULT)
  - DROP COLUMN: 테이블의 칼럼을 제거
  ```sql
  -- 컬럼 제거하기
  ALTER TABLE student DROP COLUMN phone;
  ```

### DML basics
- 테이블 내의 데이터를 조작하기 위한 언어
- INSERT, SELECT, UPDATE, DELETE

  ### SELECT
  테이블 내 데이터를 조작한다

  - SELECT: 조회한다
  ```sql
  -- first_name과 age만 뽑아서 조회 
  SELECT first_name, age FROM user;
  -- last_name, phone, email만 뽑아서 조회
  SELECT last_name, phone, email FROM user; 
  -- 전체 column 조회
  SELECT * FROM user;
  ```
  - SELECT ORDER BY: 순서를 지정하여 조회  
  (기본 오름차순, 내림차순 시 DESC 추가)
  ```sql
  -- first_name 알파벳 순으로 조회
  SELECT * FROM user ORDER BY first_name;
  -- age 순으로 조회, 같으면 first_name 순으로 조회
  -- age, first_name
  SELECT age, first_name FROM user ORDER BY age, first_name;
  -- age 역순으로 조회, 같으면 first_name 순으로 조회
  SELECT age, first_name FROM user ORDER BY age DESC, first_name;
  ```
  - SELECT DISTINCT: 중복 제거
  ```sql
  -- 나이들만 조회
  SELECT age FROM user;
  -- 중복 없이 나이를 조회
  SELECT DISTINCT age FROM user;
  ```
  - SELECT WHERE: 조건을 지정하여 해당 데이터만 조회
  ```sql
  -- 나이가 30 미만인 사람들의 first_name만 조회
  SELECT first_name FROM user WHERE age < 30;

  -- balance가 150인 사람들의 나이 조회
  SELECT age FROM user WHERE balance = 150;

  -- AND OR
  -- balance가 150 이상이면서 나이가 30 미만인 사람들을 조회
  SELECT * FROM user WHERE balance >= 150 AND age < 30;

  -- first_name이 Zelda인 사람들만 조회
  SELECT * FROM user WHERE first_name = 'Zelda';
  ```
  - SELECT WHERE LIKE: 문자열 비교 조회
  ```sql
  -- first_name이 A로 시작하는 사람들만 조회
  SELECT * FROM user WHERE first_name LIKE 'A%';

  -- first_name이 A로 시작하는 사람들 중 이름이 4글자로 이루어진 사람들만 조회
  -- _ = 1개의 문자와 동일함
  SELECT * FROM user WHERE first_name LIKE 'A___';

  -- email이 google.com인 사람
  SELECT * FROM user WHERE email LIKE '%google.com';
  -- 이름은 A로 시작하고 성은 C로 시작하는 사람
  SELECT * FROM user WHERE first_name LIKE 'A%' AND last_name LIKE 'C%';
  -- phone이 010으로 시작하지 않는 사람
  SELECT * FROM user WHERE phone NOT LIKE '010-%';
  ```

  ### INSERT
  데이터를 추가할 때 사용한다  
  ```sql
  INSERT INTO users(first_name, last_name, age, balance)
  VALUES ('sieun', 'lee', 99, 100);
  ```
  > 한번에 여러 데이터를 입력할 수도 있다.

  ### UPDATE
  기존 데이터를 새로운 값으로 변경한다
  ```sql
  UPDATE users
  SET phone = '010-1111-1111',
      age = 50
  WHERE first_name = 'sieun'; --'sieun' 이라는 사용자의 연락처와 나이를 변경      
  ```
  >WHERE를 생략할 경우 테이블 전체가 수정되니 주의

  ### DELETE
  데이터를 삭제한다
  ```sql
  DELETE FROM users
  WHERE first_name = 'sieun';
  ```

## Aggregate Functions
 - 여러 열의 데이터를 모아 특정 칼럼에 대해 집계한다
    - COUNT(): 갯수
    - AVG(): 평균
    - MAX(): 최대
    - MIN(): 최소
    - SUM(): 합계
    ```sql
    SELETE COUNT(*) FROM user;
    SELETE AVG(balance) FROM user;
    SELETE MAX(age) FROM user;
    SELETE MIN(age) FROM user;
    SELETE SUM(balance) FROM user;
    ```
    > WHERE 절을 추가하면 특정 행들에 대한 데이터만 집계 가능하다
  ### GROUP BY
  - WHERE 절은 특정한 데이터를 가지고 있는 행들에 대해서만 집계가 가능하다
  - `GROUP BY`를 사용하면 어떤 칼럼의 데이터를 기준으로 묶을 수 있다
  ```sql
  -- 국적과 국적별 평균 잔고 조회
  SELECT country, AVG(balance)
  FROM user
  -- 국적으로 그룹을 만든다
  GROUP BY country;
  ```  

  ### ORDER BY
  - 결과를 정렬해 준다
  - 역순은 `DESC`

### HAVING
- 집계 결과를 바탕으로 조회 조건을 만들 수 있다
```sql
SELECT country, AVG(age)
FROM user
GROUP BY country
-- 나이 평균이 40 미만인 나라들을 조회
HAVING AVG(age) < 40;
```
  
  






