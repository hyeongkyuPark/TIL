# DB 기본개념
## 테이블(Table)
- 데이터를 저장해놓고 꺼내 쓰는 장소로 데이터를 담고 있음
- 열/필드/Column, 행/레코드/Row 로 구성
- 데이터의 종류는 정해져 있음 (문자-varchar, 숫자-int, 날짜-date 등)
### 테이블 생성
  ```
  CREATE TABLE TEST_TABLE (
    ID VARCHAR PRIMARY KEY
    NAME VARCHAR NOT NULL
    AGE INT NOT NULL
    CREATED_AT DATE
    UPDATED_AT DATE
  )
  ```
- 제약조건
  - NOT NULL : Null(실제로 어떤 값이 있는지 알 수 없음)값이 없는 것을 의미
  - 기본키(Primary key) : 해당 테이블에 값을 구분할 수 있는 유일한 값 (거래 테이블을 예로들면 각 거래의 고유 값인 거래번호라는 필드를 기본키로 사용 가능)
  - 외래키(Foreign key) : 다른 테이블의 기본키를 참조하는 키로 테이블을 정규화하면서 테이블을 분리시킬 때 테이블을 서로 연결 시켜줌
- Relational
  - 테이블 사이에는 관계가 있음 
  - 1:1, 1:N 관계를 가질 수 있음
