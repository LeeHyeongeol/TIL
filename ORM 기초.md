# ✍ ORM

Obect-Relational Mapping의 약자로 쉽게 이해하자면 Model과 DB를 통역하는 역할을 말한다.
앞서 MVC 퍠턴을 공부하면서 view-controller-model의 관계를 이해했었다.
DB가 sql이기 때문에 model에 sql문법을 작성하고 controller의 요청에 맞게 model이 DB에서 데이터를 가져오는 형식이었다.

하지만 DB의 종류는 여러가지가 있다 MYSQL, MS-SQL, MariaDB,  mongoDB 등등..
다양한 DB를 사용하는 회사에서 일한다고 해보자. 이 때마다 model의 코드를 각 DB가 호환하는 언어로 바꿔 작성하는 일은 비효율적일 것이다.

그래서 ORM을 통해 여러 DB에 쉽게 호환될 수 있도록 model을 공통의 문법으로 통일하는 것이다.

# ✍ ORM 사용방법

앞에서 배운 클래스를 만들어 사용한다.
기존의 sql에서는 테이블을 생성하고 각 요소를 삽입하는 문구를 작성해야했다.
```jsx
CREATE TABLES HYEONGEOL
INSERT INTO HYEONGEOL(name) VALUES (hyeongeol)
```
이는 db가 sql인 경우에만 사용할 수 있으므로 다양한 db에 사용할 수 있도록 공통의 문법으로 클래스를 작성하면 된다.

```jsx
class Person() {
constructor(name){
this.name = 'hyeongeol'
}
}
const person = new Person(...)
```

![스크린샷, 2022-01-27 23-36-36](https://user-images.githubusercontent.com/68496535/151380134-d0f463b6-b3ae-4a17-beb7-f1604208ce4f.png)

# ✍ Sequelize

다양한 orm이 있다. Flask : SQLAlchemy, Django : 내장 ORM, Node.js : sequelize, Java : Hybernate,JPA, GraphQL : Prisma 등등
그 중에서 오늘 배운 sequelize에 대해 정리해보고자 한다.
우선 Node.js를 기반으로한 ORM으로 지원하는 RDBMS는 Postgres, MySQL, MariaDB, SQLite, Microsoft SQL Server 이다.





