# MVC

정보를 보다 더 전문적인 영역에서 관리하는 방법을 안내한다.
추가적으로 ORM을 활용해 DB와 프로그래밍 언어 사이의 개념 간극을 줄여준다

mvc패턴은 왜 생겨난 것일까?
mvc가 생겨나기 전, 개발자들이 코드가 많아질 수록 수정하기 어렵고 유지보수가 힘들었다.
코드를 계속 짜다보니 코드 구성 패턴을 발견했고 이것들을 공식으로 만들어 논문으로 발표한 것이 mvc 패턴이다.

즉 mvc는 유지보수가 편해지는 코드 구성 방식이다.
model : 데이터와 관련된 부분
view : 사용자한테 보여지는 부분
controller : model과 view를 이어주는 부분

# mvc를 지키면서 코딩하는 방법
#### 1. model은 controller와 view에 의존하지 않아야 한다. 쉽게 말하면 model 내부에 controller와 view에 관련된 코드가 있으면 안된다.
```jsx
public class Student {
private String name;
private int age;

public Student(String name,int age) {
this.name = name;
this.age = age;
}
public String getName() {
return name;
}
public int getAge() {
return age;
}
}
```
#### 2. view는 model에만 의존해야 하고, controller에는 의존하면 안된다. 쉽게 말하면 view 안에 model 코드만 있을 수 있고, controller 코드가 있으면 안된다.
```jsx
public class OutputView{
public void printProfile(Student student) {
System.out.printIn(
"내 이름은 " + student.getName() + "입니다.")
System.out.printIn(
"내 나이는" + student.getAge() + "입니다.")
}
}
```
#### 3. view가 model로부터 데이터를 받을때는, 사용자마다 다르게 보여줘야하는 데이터만 받아와야 한다.
#### 4. controller에는 model과 view에 의존해야하 한다. 쉽게 말하면 controller 내부에는 model과 view의 코드가 있을 수 있다.
```jsx
public class COntroller {
public static void main(String[] args){
Student student = new Student("기철",25)
OutputView.printProfile(student);
}
}
```
#### 5. view가 model로부터 데이터를 받아올 때, 반드시 controller에서 받아야 한다.

# 웹에서 mvc가 작동하는 그림

1. 사용자가 브라우저의 이벤트를 발생
2. 라우터가 엔드포인트를 분기
3. 분기된 엔드포인트가 controller로 전달
4. View로 전송 하거나 Model에 db자료를 요청하기도 한다.


