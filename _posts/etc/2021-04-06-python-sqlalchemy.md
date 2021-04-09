---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : SQLAlchemy # 제목
excerpt             : 파이썬 SQLAlchemy # 썸네일 한줄 요약
last_modified_at    : 2021-04-06 # 마지막 수정일
categories          : etc
tags                : Python SQLAlchemy
toc                 : # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---

---
## 출처 [SQLAlchemy tutorial](https://docs.sqlalchemy.org/en/14/tutorial/engine.html)

🚫 아래 내용은 주관적인 생각이므로 사실과 다를 수 있습니다.


사용 언어 파이썬

## 모듈 설치

```
# IOX
python -m pip install sqlalechmy
```
`-m`을 꼭 붙여줘야된다

---

## 연결 설정 - 엔진

```py
from sqlalchemy import create_engine
engine = create_engine("DB종류+DBAPI(드라이버)종류://아이디:비번@호스트/DB이름", 옵션들,,,)
```

본문 예시의 경우 sqlite3 인메모리 DB를 사용했다
```py
from sqlalchemy import create_engine

engine = create_engine("sqlite+pysqlite:///:memory:", echo=True, future=True)
```

---


## 연결하기

```py
from sqlalchemy import text

with engine.connect() as conn:
    result = conn.execute(text("select 'hello world'"))
    print(result.all())
```
위와 같이 실행하더라도 커밋을 하지 않으면 변경사항이 실제로 적용되진 않는다
---

## 변경사항 커밋

```py
with engine.connect() as conn:
    conn.execute(text("CREATE TABLE some_table (x int, y int)"))
    conn.execute(
        text("INSERT INTO some_table (x, y) VALUES (:x, :y)"),
        [{"x": 1, "y": 1}, {"x": 2, "y": 4}]
    )
    conn.commit()
```

위와 같이 쿼리문을 connection 객체의 execute() 함수로 넘겨주기만 하면 실행이 되고  
commit() 함수로 커밋을 한다

그러나 커밋함수를 호출하지 않고 커밋하는 방법도 있다

```py
with engine.begin() as conn:
    conn.execute(
        text("INSERT INTO some_table (x, y) VALUES (:x, :y)"),
        [{"x": 6, "y": 8}, {"x": 9, "y": 10}]
    )
```

위와 같이 connect 대신 begin() 함수를 사용하면  
블록 내의 모든 쿼리문들에서 예외가 발생하지 않았다면 마지막에 커밋을 수행해준다

---

## 실행 구문의 기초

### 행 가져오기

위의 코드들에서 추가한 행들을 가져와 출력해보자

```py
with engine.connect() as conn:
    result = conn.execute(text("SELECT x, y FROM some_table"))
    for row in result:
        print(f"x: {row.x}  y: {row.y}")
```

`SELECT`로 선택해 가져온 결과물들이 이터러블하다는걸 알 수 있다

result.all()은 행을 전부 다 가져온다  
이 또한 이터레이터 인터페이스를 구현했기 때문에 순환이 가능하다

이 행 객체들은 네임드 튜플처럼 접근할 수도 있다

- 튜플 할당
```py
for x, y in result:
```

- 인덱스
```py
for row in result:
      x = row[0]
```

- 네임드 튜플
  네임드 튜플의 속성처럼 컬럼명을 그대로 사용 가능하다
```py
for row in result:
    y = row.y

    # illustrate use with Python f-strings
    print(f"Row: {row.x} {row.y}")
```

- 매핑 접근
  Result.mappings() 함수를 사용하면 dict 객체와 비슷하지만  
  읽기만 가능한 MappingResult 객체로 받을 수도 있다
```py
for dict_row in result.mappings():
    x = dict_row['x']
    y = dict_row['y']
```

---

## 인자 보내기

Connection.execute() 함수는 쿼리문에서 변수를 참조하면 참조한 변수를 인자로 받는다

```py
with engine.connect() as conn:
    result = conn.execute(
        text("SELECT x, y FROM some_table WHERE y > :y"),
        {"y": 2}
    )
    for row in result:
       print(f"x: {row.x}  y: {row.y}")
```

아래와 같이 인자를 여러개 보낼수도 있다
```py
text("INSERT INTO some_table (x, y) VALUES (:x, :y)"),
[{"x": 11, "y": 12}, {"x": 13, "y": 14}]
```

이게 불편하면 TextClause.bindparams() 함수로 직접 바인딩해줄수도 있다
```py
text("SELECT x, y FROM some_table WHERE y > :y ORDER BY x, y")
.bindparams(y=6)
```
인자를 하나(y)만 보내도 로그를 보면 튜플로 찍힌다

---

## ORM 세션으로 실행

```py
from sqlalchemy.orm import Session

stmt = text("SELECT x, y FROM some_table WHERE y > :y ORDER BY x, y").bindparams(y=6)
with Session(engine) as session:
    result = session.execute(stmt)
    for row in result:
       print(f"x: {row.x}  y: {row.y}")
```

SQLAlchemy에서는 DB 핸들을 세션이라고한다  
주로 Connection 객체와 유사하게 사용되며, 실제로 세션은 내부적으로 SQL을 보낼 때 Connection 객체를 참조한다

```py
# 사용예시
from sqlalchemy.orm import Session

stmt = text("SELECT x, y FROM some_table WHERE y > :y ORDER BY x, y").bindparams(y=6)
with Session(engine) as session:
    result = session.execute(stmt)
    for row in result:
       print(f"x: {row.x}  y: {row.y}")

...

with Session(engine) as session:
    result = session.execute(
        text("UPDATE some_table SET y=:y WHERE x=:x"),
        [{"x": 9, "y":11}, {"x": 13, "y": 15}]
    )
    session.commit()
```

---


## 메타 데이터 설정

관계형 DB를 사용할 때의 기본 구성은 table이다  
SQLAlchemy에서 table은 파이썬의 Table 객체로 표현된다  
각 Table 객체는 하나하나 명시적으로 그 구성을 기재할수도 있고  
이미 존재하는 특정 DB의 객체들을 반영할 수도 있다  
두 가지 방식을 혼합하는것도 가능하다  

둘 중 어떤 방식을 사용하더라도 여러 DB 설정을 담고 있는 MetaData 객체부터 시작해야한다
MetaData 객체의 구성방식은 다음과 같다

```py
from sqlalchemy import MetaData

metadata = MetaData()
```

MetaData 객체는 앱 전체에서 하나만,  
models 또는 dbschema 패키지 중 한 곳에서 모듈 레벨 변수로 사용되는게 일반적이다  
여러개를 쓸 수도 있지만, 여러 Table 객체들이 모두 한 곳으로 연결되는게 가장 쓰기 편하다

MetaData 객체가 생겼으면 이제 다음과 같이 Table 객체들을 선언 할 수 있다
```py
from sqlalchemy import Table, Column, Integer, String

user_table = Table(
    "user_account",
    metadata,
    Column('id', Integer, primary_key=True),
    Column('name', String(30)),
    Column('fullname', String)
)
```

보면 SQL CREATE TABLE 구문이랑 비슷하다  
아무튼 임포트해서 사용하는 객체들을 둘러보자면
  - Table: DB 테이블을 나타내며 자신을 MetaData 컬렉션에 할당
  - Column: DB 테이블의 열을 나타내며 자신을 Table 객체에 할당
    - 일반적으로 상위 Table 객체의 Table.c에 있는 연관 배열을 통해 엑세스 된다
      ex) user_table.c.keys() -> ['id', 'name', 'fullname']
  - Integer, String: SQL 데이터 타입을 나타내며 인스턴스화 여부와 관계없이 Column으로 전달 가능하다

---

## 외부키 설정

```py
from sqlalchemy import ForeignKey

address_table = Table(
    "address",
    metadata,
    Column('id', Integer, primary_key=True),
    Column('user_id', ForeignKey('user_account.id'), nullable=False),
    Column('email_address', String, nullable=False)
)
```
외부키(ForeignKey)로 지정하면 데이터타입을 생략해도  
자동으로 해당 연관 열의 데이터 타입을 가져와 추론한다  

---

## MetaData로 DB 테이블 초기화 (DDL 보내기)

DDL: Data Definition Language
```py
metadata.create_all(engine)
```

---

## ORM으로 Table 메타 데이터 선언하기

방금 위에서 했던 테이블 설정들을 ORM을 이용해서 다시 해보자

### Registry 설정

```py
from sqlalchemy.orm import registry

mapper_registry = registry()
```

위와 같이 레지스트리를 생성하면 테이블을 저장할 메타데이터를 자동으로 생성해 그 안에 가지게 됩니다

```py
mapper_registry.metadata -> MetaData()
```

Table 객체를 직접 선언하는것 대신에 declarative base를 이용해 간접적으로 선언한다  
declarative base는 registry.generate_base() 함수로 얻을 수 있다  

```py
Base = mapper_registry.generate_base()
```

레지스트리를 선언하고 declarative base를 반환받는 것은 declarative_base()로 한번에 대체할 수 있다
```py
from sqlalchemy.orm import declarative_base

Base = declarative_base()
```

## ORM 매핑된 클래스 선언

```py
from sqlalchemy.orm import relationship

class User(Base):
    __tablename__ = 'user_account'

    id = Column(Integer, primary_key=True)
    name = Column(String(30))
    fullname = Column(String)

    addresses = relationship("Address", back_populates="user")

    def __repr__(self):
        return f"User(id={self.id!r}, name={self.name!r}, fullname={self.fullname!r})"

class Address(Base):
    __tablename__ = 'address'

    id = Column(Integer, primary_key=True)
    email_address = Column(String, nullable=False)
    user_id = Column(Integer, ForeignKey('user_account.id'))

    user = relationship("User", back_populates="addresses")

    def __repr__(self):
        return f"Address(id={self.id!r}, email_address={self.email_address!r})"
```

위의 두 클래스는 매핑된 클래스다  
이제 ORM 영속성 및 쿼리에 이용될 수 있다  
그리고 \_\_table\_\_ 속성을 이용해 아래와 같은 테이블 정보들을 확인할 수 있다

```py
print(User.__table__)

# 아래는 출력 결과물
Table('user_account', MetaData(),
    Column('id', Integer(), table=<user_account>, primary_key=True, nullable=False),
    Column('name', String(length=30), table=<user_account>),
    Column('fullname', String(), table=<user_account>), schema=None)
```

### 사용 팁

- 매핑된 클래스는 기본 생성자가 제공된다
```py
sandy = User(name="sandy", fullname="Sandy Cheeks")
```

- 누락된 항목은 예외 대신 None을 넣어 반환해준다
```py
print(sandy)

# 출력 결과물
User(id=None, name='sandy', fullname='Sandy Cheeks')
```

- 위의 두 매핑된 클래스에는 양방향 관계 설정(one to many / many to one)이 되어있다

---

## ORM으로 DB 테이블 초기화 (DDL 보내기)

```py
Base.metadata.create_all(engine)
```

---

## 코어 테이블 선언과 ORM 선언

아래는 하이브리드 테이블이라고하며 선언적 프로세스에서 생성하는 대신  
.__ table__ 속성에 직접 할당해 구성한다
```py
class User(Base):
    __table__ = user_table

     addresses = relationship("Address", back_populates="user")

     def __repr__(self):
        return f"User({self.name!r}, {self.fullname!r})"

class Address(Base):
    __table__ = address_table

     user = relationship("User", back_populates="addresses")

     def __repr__(self):
         return f"Address({self.email_address!r})"
```

이 두 클래스는 위의 ORM 매핑된 클래스들과 동등하다

\_\_tablename\_\_을 사용해 Table 객체를 자동생성하는 기존의 declarative base 방식이 가장 대중적으로 쓰인다

---

## 삽입 쿼리문

```py
from sqlalchemy import insert

stmt = insert(user_table).values(name='spongebob', fullname="Spongebob Squarepants")
```

insert() 함수에 테이블 변수를 넣고 삽입할 값들을 values() 함수에 넣어주면 쿼리문이 생성된다

```py
compiled = stmt.compile()
print(compiled.params)

# 출력 결과물
{'name': 'spongebob', 'fullname': 'Spongebob Squarepants'}
```

## 실행

```py
with engine.connect() as conn:
    result = conn.execute(stmt)
    conn.commit()
```

결과물로는 보통 해당 행의 primary key를 반환한다  
result.inserted_primary_key와 같은 방식으로 접근이 가능

여러줄을 삽입할 수도 있다
```py
with engine.connect() as conn:
    result = conn.execute(
        insert(user_table),
        [
            {"name": "sandy", "fullname": "Sandy Cheeks"},
            {"name": "patrick", "fullname": "Patrick Star"}
        ]
    )
    conn.commit()
```

### 좀 더 알아보기

식별키를 몰라도 찾아서 쓰면 된다

```py
from sqlalchemy import select, bindparam

scalar_subquery = (
    select(user_table.c.id).
    where(user_table.c.name==bindparam('username')).
    scalar_subquery()
)
with engine.connect() as conn:
    result = conn.execute(
        insert(address_table).values(user_id=scalar_subquery),
        [
            {"username": 'spongebob', "email_address": "spongebob@sqlalchemy.org"},
            {"username": 'sandy', "email_address": "sandy@sqlalchemy.org"},
            {"username": 'sandy', "email_address": "sandy@squirrelpower.org"},
        ]
    )
    conn.commit()
```

## INSERT - FROM SELECT

SELECT로 반환된 객체에 별 다른 변환없이 바로 Insert.from_select() 함수를 써서  
INSERT 구문을 구성할 수 있다

```py
select_stmt = select(user_table.c.id, user_table.c.name + "@aol.com")
insert_stmt = insert(address_table).from_select(
    ["user_id", "email_address"], select_stmt
)
```

## INSERT - RETURNING

RETURNING 구문은 보통 마지막으로 삽입 된 PK 값과 서버 PK 값을 검색하기 위해 자동으로 사용된다  
그러나 Insert.returning() 함수를 써서 명시적으로 지정할 수도 있다  
아래의 구문을 실행하면 접근 가능한 행이 담긴 Result 객체가 반환된다

```py
insert_stmt = insert(address_table).returning(address_table.c.id, address_table.c.email_address)
print(insert_stmt)
```

추가로 위의 Insert.from_select() 함수와 함께 사용할 수도 있다

```py
select_stmt = select(user_table.c.id, user_table.c.name + "@aol.com")
insert_stmt = insert(address_table).from_select(
    ["user_id", "email_address"], select_stmt
)
print(insert_stmt.returning(address_table.c.id, address_table.c.email_address))
```

### 팁

- RETURNING 기능은 UPDATE 또는 DELETE 구문도 지원한다
- 다만 일반적으로는 단일 인자로만 지원하고 다중인자는 작동하지 않는다


## 데이터 선택

Core와 ORM 모두 select() 함수로 SELECT 쿼리에 사용되는 Select 구문을 생성해
Core의 Connection.execute() 또는 ORM의 Session.execute()와 같은 함수들로 전달한다
그럼 현재 트랜잭션에서 SELECT 구문을 방출되고 반환된 Result 객체를 통해 결과물에 접근이 가능하다

## select() 함수

insert() 함수와 동일한 방법으로 사용한다

```py
from sqlalchemy import select

stmt = select(user_table).where(user_table.c.name == 'spongebob')
print(stmt)

# 출력 결과물
SELECT user_account.id, user_account.name, user_account.fullname
FROM user_account
WHERE user_account.name = :name_1
```

SELECT 반환값은 반복문으로 순환이 가능하다
```py
# Connection 순환
stmt = select(user_table).where(user_table.c.name == 'spongebob')
with engine.connect() as conn:
    for row in conn.execute(stmt):
        print(row)
# 출력 결과물
(1, 'spongebob', 'Spongebob Squarepants')


# Session 순환
stmt = select(User).where(User.name == 'spongebob')
with Session(engine) as session:
    for row in session.execute(stmt):
        print(row)
# 출력 결과물
(User(id=1, name='spongebob', fullname='Spongebob Squarepants'),)
```

## Column과 FROM 구문

테이블 째로 선택하면 전체를 가져온다
```py
print(select(user_table))

# 출력 결과물
SELECT user_account.id, user_account.name, user_account.fullname
FROM user_account
```

부분만 가져오려면 원하는 항목들만 인자로 넘겨주면 된다
```py
print(select(user_table.c.name, user_table.c.fullname))

# 출력 결과물
SELECT user_account.name, user_account.fullname
FROM user_account
```

## ORM 엔티티와 Column 선택

엔티티 자체 또한 선택이 가능하다
```py
# 엔티티 출력
print(select(User))
# 출력 결과물
SELECT user_account.id, user_account.name, user_account.fullname
FROM user_account

# 엔티티 중 첫번째 행 출력
session.execute(select(User)).first()

# 엔티티 중 첫번째 행 중 부분 지정 열들 출력
session.execute(select(User.name, User.fullname)).first()
```

이러한 방식들은 아래와 같이 섞어서 쓸 수도 있다
```py
session.execute(
    select(User.name, Address).
    where(User.id==Address.user_id).
    order_by(Address.id)
).all()
```

[ORM 엔티티, 속성 선택 쿼리 가이드](https://docs.sqlalchemy.org/en/14/orm/queryguide.html#orm-queryguide-select-columns)

## 선택 항목에 라벨 붙이기

```py
from sqlalchemy import func, cast

stmt = (
    select(
        ("Username: " + user_table.c.name).label("username"),
    ).order_by(user_table.c.name)
)
with engine.connect() as conn:
    for row in conn.execute(stmt):
        print(f"{row.username}")

# 출력 결과물
Username: patrick
Username: sandy
Username: spongebob
```

## WHERE 구문

파이썬 비교문을 쿼리 비교문으로 변환해준다
```py
print(user_table.c.name == 'squidward')
user_account.name = :name_1 # 출력 결과물

print(address_table.c.user_id > 10)
address.user_id > :user_id_1 # 출력 결과물
```

변환된 쿼리 비교문을 Select.where() 함수로 바로 전달 가능하다
```py
print(select(user_table).where(user_table.c.name == 'squidward'))
# 츌력 결과물
SELECT user_account.id, user_account.name, user_account.fullname
FROM user_account
WHERE user_account.name = :name_1
```

중첩 또한 가능하다
```py
print(
    select(address_table.c.email_address).
    where(user_table.c.name == 'squidward').
    where(address_table.c.user_id == user_table.c.id)
)
# 츌력 결과물
SELECT address.email_address
FROM address, user_account
WHERE user_account.name = :name_1 AND address.user_id = user_account.id
```

Select.where() 함수는 다중 조건도 수용한다
```py
print(
    select(address_table.c.email_address).
    where(
         user_table.c.name == 'squidward',
         address_table.c.user_id == user_table.c.id
    )
)
# 출력 결과물
SELECT address.email_address
FROM address, user_account
WHERE user_account.name = :name_1 AND address.user_id = user_account.id
```

물론 인자로 and\_()와 or\_() 함수도 사용이 가능하다
```py
from sqlalchemy import and_, or_
print(
    select(Address.email_address).
    where(
        and_(
            or_(User.name == 'squidward', User.name == 'sandy'),
            Address.user_id == User.id
        )
    )
)
# 출력 결과물
SELECT address.email_address
FROM address, user_account
WHERE (user_account.name = :name_1 OR user_account.name = :name_2)
AND address.user_id = user_account.id
```

단일 엔티티의 간단한 동일여부 확인에는 아래의 Select.filter_by() 함수도 많이 사용된다
```py
print(
    select(User).filter_by(name='spongebob', fullname='Spongebob Squarepants')
)
# 출력 결과물
SELECT user_account.id, user_account.name, user_account.fullname
FROM user_account
WHERE user_account.name = :name_1 AND user_account.fullname = :fullname_1
```

[SQLAlchemy의 연산자들](https://docs.sqlalchemy.org/en/14/core/operators.html)

## 명시적 FROM과 JOIN

일반적으로 선택할 항목에 대해 특별한 언급이 없다면 출처를 알아서 추론한다
```py
print(select(user_table.c.name))
# ㅊㄹ ㄱㄱㅁ
SELECT user_account.name
FROM user_account
```

테이블이 달라도 각각 잘 가져온다
```py
print(select(user_table.c.name, address_table.c.email_address))
# ㅊㄹ ㄱㄱㅁ
SELECT user_account.name, address.email_address
FROM user_account, address
```

조인하는 방법은 일반적으로 두 가지 중 하나를 쓴다  

첫번째는 조인의 왼쪽 테이블과 오른쪽 테이블을 명시적으로 지정할 수 있는  
Select.join_from() 함수다
```py
print(
    select(user_table.c.name, address_table.c.email_address).
    join_from(user_table, address_table)
)
# ㅊㄹ
SELECT user_account.name, address.email_address
FROM user_account JOIN address ON user_account.id = address.user_id
```

두 번째는 오른쪽만 지정하고 왼쪽은 추론하는 Select.join() 함수다
```py
print(
    select(user_table.c.name, address_table.c.email_address).
    join(address_table)
)
# ㅊㄹ
SELECT user_account.name, address.email_address
FROM user_account JOIN address ON user_account.id = address.user_id
```

Select.select_from() 함수로 선택 항목들의 범위(SQL에서의 ON)를 지정할 수 있다  
```py
print(
    select(address_table.c.email_address).
    select_from(user_table).join(address_table)
)
# ㅊㄹ
SELECT address.email_address
FROM user_account JOIN address ON user_account.id = address.user_id
```


네이티브 쿼리 SELECT count(*)는 sqlalchemy.sql.expression.func 모듈의  
func.count('*') 함수로 표현할 수 있다
```py
from sqlalchemy import func
print (
    select(func.count('*')).select_from(user_table)
)
# print
SELECT count(:count_2) AS count_1
FROM user_account
```

## ON 구문 설정

Select의 join()과 join_from() 함수 둘 다  
아래와 같이 ON 구문을 위한 추가 인자 전달을 지원한다  

```py
print(
    select(address_table.c.email_address).
    select_from(user_table).
    join(address_table, user_table.c.id == address_table.c.user_id)
)
# print
SELECT address.email_address
FROM user_account JOIN address ON user_account.id = address.user_id
```

## OUTTER와 FULL join

.join()과 join_from() 모두 키워드 인자로  
각각 SQL의 LEFT OUTER JOIN, FULL OUTER JOIN의 역할을 하는  
Select.joind의 .isouter와 .full을 지원한다  

```py
print(  
    select(user_table).join(address_table, isouter=True)
)
# print
SELECT user_account.id, user_account.name, user_account.fullname
FROM user_account LEFT OUTER JOIN address ON user_account.id = address.user_id
# .join(..., isouter=True) 대신 .outerjoin(...)를 써도 된다

print(
    select(user_table).join(address_table, full=True)
)
# print
SELECT user_account.id, user_account.name, user_account.fullname
FROM user_account FULL OUTER JOIN address ON user_account.id = address.user_id
```

### 팁

SQL에는 RIGHT OUTER JOIN이 있지만 SQLAlchemy에는 없다  
대신 LEFT OUTER JOIN을 하고 테이블들을 역순으로 정렬하면 된다

## ORDER BY

Select.order_by() 함수로 아래와 같이 정렬이 가능하다
```py
print(select(User).order_by(User.name.asc(), User.fullname.desc()))
# print
SELECT user_account.id, user_account.name, user_account.fullname
FROM user_account ORDER BY user_account.name ASC, user_account.fullname DESC
```


Group by...

```py
with engine.connect() as conn:
    result = conn.execute(
        select(User.name, func.count(Address.id).label("count")).
        join(Address).
        group_by(User.name).
        having(func.count(Address.id) > 1)
    )
    print(result.all())

# print
BEGIN (implicit)
SELECT user_account.name, count(address.id) AS count
FROM user_account JOIN address ON user_account.id = address.user_id GROUP BY user_account.name
HAVING count(address.id) > ?
[...] (1,)
```