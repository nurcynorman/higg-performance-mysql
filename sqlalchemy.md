create simple db

```python
from sqlalchemy import create_engine , Column , Integer, String 
from sqlalchemy.ext.declarative import declarative_base 
from sqlalchemy.orm import sessionmaker 

engine = create_engine('sqlite:///example.db', echo=True)

Base = declarative_base()

class User(Base):
    __tablename__ = 'users'

    id = Column(Integer, primary_key=True)
    name = Column(String)
    email = Column(String)

    def __repr__(self):
        return f"<User(name={self.name}, email={self.email})>"
    
Base.metadata.create_all(engine)

Session = sessionmaker(bind=engine) 
session = Session()

user1 = User(name='Alice', email='alice@example.com')
user2 = User(name='Bob', email='bob@example.com')

session.add(user1)
session.add(user2)
session.commit()

users = session.query(User).all()
for user in users:
    print(user)
```
