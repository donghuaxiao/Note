## SqlAlchemy

### 定义table 和 实体类的映射
对于ORM 数据库操作来说主要是要定义 Table 和 实体类的映射关系， 实体类的字段和表的对于关系

#### 1. Declarative Mapping
在声明时映射中，对象和 Table 使用同一个类来表示，在类中定义表的字段。 通过工厂函数 declarative_base() 创建一个基类 Base, 在Base 中定义了构造函数
```__init__(self, **kwargs)```, 使用dict 来保存和表的对应关系。

```
  from sqlalchemy.orm import declarative_base
  Base = declarative_base()
  
  class User(Base):
    __tablename__ = 'user'
    id = Column( Integer, primary_key=True)
    name = Column( String(20) )
    fullname = Column( String(40) )
    
  user = User(name='test', fullname='test_test')
```
这样通过字典的key 和 类 User 的 属性名 构成了对象和 表字段的映射关系。

#### 2. Classicl Mapping
经典映射 要定义 Table 和 实体类， 然后把两者映射起来。

```
  from sqlalchemy import Table, MetaData, Column, String, Integer
  from sqlalchemy.orm import mapper
  
  metadata = MetaData()
  user = Table('user', metadata,
      Column('id', Integer, primary_key=True),
      Column('name', String(20) ),
      Column('fullname', String(40) )
      
  class User(object):
    def __init__(self, name, fullname ):
      self.name = name
      self.fullname = fullname
      
  mapper( User, user)
```
