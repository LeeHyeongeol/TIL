# ✍ SQL 이란?

Structured Query Language의 약어로 주로 관계형 데이터베이스에서 사용한다.

데이터베이스 전용 프로그래밍 언어이며, 데이터베이스에 쿼리를 보내 원하는 데이터를 가져오거나 삽입할 수 있다.

말그대로 구조화된 데이터에 조건을 달아 다루는 것이므로 데이터 구조가 고정되어야 하는 특징을 가진다.

# ✍ SQL 기본문법
데이터베이스 생성 접근 방법
```jsx
CREATE DATABASE 데이터베이스 이름 //db생성
USE 데이터베이스 이름 //db접근
DESC 테이블이름 //db 안의 테이블에 접근
```
테이블 생성 방법
```ts
CREATE TABLE `content_category` (
  `id` int PRIMARY KEY AUTO_INCREMENT,
  `contentId` int NOT NULL,
    FOREIGN KEY (`contentId`) REFERENCES `content` (`id`),
  `categoryId` int NOT NULL,
  FOREIGN KEY (`categoryId`) REFERENCES `category` (`id`)
);
```
데이터베이스 명령어는 많기 때문에 직접 문제를 풀어보면서 익히는게 효율적이라고 생각한다.
```jsx
SELECT
FROM
WHERE
ORDER BY
DESC
LIMIT
DISTINCT
INNER JOIN
ORDER JOIN
```

연습자료 : https://www.w3schools.com/sql/sql_exercises.asp


# ✍ SQL 문법 연습

```jsx
SELECT * FROM user WHERE user.name
//user테이블 name 컬럼을 모두 조회

INSERT INTO user (name,email) VALUES ('hyeongeol','dlgusrjf@naver.com')
// user 테이블 name 컬럼에 hyeongeol, email 컬럼에 dlgusrjf@naver.com을 추가.
SELECT content.title, user.name FROM content 
LEFT JOIN user ON user.id = content.userId
//content 테이블의 title 컬럼과 user 테이블의 name 컬럼을 조회한다. user 테이블의 name 컬럼이 없어도 title을 찾아야 한다.
SELECT content.title, user.name FROM content
LEFT JOIN user
ON user.id = content.userId
WHERE user.name IS NOT NULL 
//content 테이블의 title 컬럼과 user 테이블의 name 컬럼을 조회한다. 단 user 테이블의 name이 NULL이 아닌 title만 찾아야 한다.
UPDATE content SET body = 'database is very easy' WHERE content.title = 'database sprint' 
//content 테이블의 title 컬럼이 database sprint인 body 컬럼을 database is very easy로 수정한다.
INSERT INTO content  (title,body,created_at,userId) VALUES ('k','kk',now(),'1')



```
