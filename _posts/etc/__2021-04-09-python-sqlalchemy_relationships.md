---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : SQLAlchemy 관계설정 # 제목
excerpt             : 파이썬 SQLAlchemy 관계설정 # 썸네일 한줄 요약
last_modified_at    : 2021-04-09 # 마지막 수정일
categories          : etc
tags                : Python SQLAlchemy ORM Relationship
toc                 : # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---

---
## 출처 [SQLAlchemy ORM](https://docs.sqlalchemy.org/en/14/orm/basic_relationships.html?highlight=relationship)

🚫 아래 내용은 주관적인 생각이므로 사실과 다를 수 있습니다.


사용 언어 파이썬

### imports

```py
from sqlalchemy import Table, Column, Integer, ForeignKey
from sqlalchemy.orm import relationship
from sqlalchemy.ext.declarative import declarative_base

Base = declarative_base()
```

## One To Many

일 대 다 (One To Many) 관계설정  
편의상 아래의 부모 자식으로 예를 들겠다  
```py
class Parent(Base):
    __tablename__ = 'parent'
    id = Column(Integer, primary_key=True)
    children = relationship("Child") # added 자식들을 가리킴

class Child(Base):
    __tablename__ = 'child'
    id = Column(Integer, primary_key=True)
    parent_id = Column(Integer, ForeignKey('parent.id')) # added 부모를 가리킴
```
위 코드는 각각의 단방향 관계가 설정된 것이지 양방향 관계가 아니다

양방향 관계를 설정하려면 다음과 같이 명시해주면 된다
```py
class Parent(Base):
    __tablename__ = 'parent'
    id = Column(Integer, primary_key=True)
    children = relationship("Child", back_populates="parent") # edited

class Child(Base):
    __tablename__ = 'child'
    id = Column(Integer, primary_key=True)
    parent_id = Column(Integer, ForeignKey('parent.id'))
    parent = relationship("Parent", back_populates="children") # added
```

부모가 삭제되었을때 연관된 모든 자식들도 함께 삭제하는 방법에 대해서는  
다음의 링크들에서 확인바란다
- [delete](https://docs.sqlalchemy.org/en/14/orm/cascades.html#cascade-delete)
- [Using foreign key ON DELETE cascade with ORM relationships](https://docs.sqlalchemy.org/en/14/orm/cascades.html#passive-deletes)
- [delete-orphan](https://docs.sqlalchemy.org/en/14/orm/cascades.html#cascade-delete-orphan)


## Many To One

