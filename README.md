# 2. 개발환경 및 개발언어
## 2-1. 개발언어
![java](http://img1.daumcdn.net/thumb/R1920x0/?fname=http%3A%2F%2Fcfile27.uf.tistory.com%2Fimage%2F2550B64D5905584E08FFEE)

팀원들이 공통적으로 잘 다룰 수 있는 java를 기본적인 개발언어로 사용한다. java는 jvm위에서 동작하는 언어로, 학교에서 가르치는 대표적 객체지향언어, gc등을 통해 개발자에게 메모리관리 등을 편하게 해준다. jdk 1.8을 이용하여 작업하며, 공식문서(https://docs.oracle.com/javase/8/docs/api/)를 참조한다.

![javascript](http://img1.daumcdn.net/thumb/R1920x0/?fname=http%3A%2F%2Fcfile26.uf.tistory.com%2Fimage%2F2263484D5905584E0D48F7)

인기짱짱! 대세언어! js를 사용한다. js는 웹브라우저에서 동적효과를 줄 때 사용하며, 반응형 웹의 각종 컴포넌트와 api서버에서 받아올 때도 쓰인다. 정리가 잘되어있는 reference(https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference)를 참조한다.

## 2-1. API 서버
![spring](http://img1.daumcdn.net/thumb/R1920x0/?fname=http%3A%2F%2Fcfile10.uf.tistory.com%2Fimage%2F22103B4D590558500B50F8) ![redis](http://img1.daumcdn.net/thumb/R1920x0/?fname=http%3A%2F%2Fcfile28.uf.tistory.com%2Fimage%2F2271EB4D5905585007D493)

java기반의 스프링 프레임워크 4.x를 Restful API서버 구축에 사용한다. 메이븐 등을 통해 어플리케이션 단위로 인프라를 관리할 수 있고, 비즈니스 로직에 집중할 수 있다. 또한 Jackson2를 이용하여 보다 쉽게 json으로 통신하고자 한다. 챗봇의 경우, 기본적으로 키/값 형태로 대화하므로 많은 부하에도 빠른 대응을 위해 오픈소스 인메모리DB인 Redis를 사용한다

## 2-2. 호스팅
![aws](http://img1.daumcdn.net/thumb/R1920x0/?fname=http%3A%2F%2Fcfile29.uf.tistory.com%2Fimage%2F2529E74D5905584B104BC8)

클라우드 서비스인 AWS를 배포하는 서버로 이용하고자 한다. EC2서비스인 AWS ubuntu 16.04 LTS를 이용한다.

## 2-3. 클라이언트
## 2-3-1. 챗봇
![yellowID](http://img1.daumcdn.net/thumb/R1920x0/?fname=http%3A%2F%2Fcfile5.uf.tistory.com%2Fimage%2F250E484C590558510A4912)

카카오톡 플랫폼에서 서비스할 예정이므로 Yellow ID를 사용한다. 유저는 카카오톡 옐로우아이디를 통해 메세지를 주고 받으며 대화할 수 있다. 공식 문서(https://github.com/plusfriend/auto_reply)를 참조한다.

## 2-3-2. 반응형 웹
![react](http://img1.daumcdn.net/thumb/R1920x0/?fname=http%3A%2F%2Fcfile24.uf.tistory.com%2Fimage%2F26617B45590558E91F397F)
![bootstrap](http://img1.daumcdn.net/thumb/R1920x0/?fname=http%3A%2F%2Fcfile28.uf.tistory.com%2Fimage%2F212A484D5905584C0463D5)

프론트엔드에 UI를 위한 JS라이브러리인 React.js를 사용한다. flux로 예측이 좀더 가능하도록 코드를 구조화하고, CSS는 Bootstrap을 이용하여 모던하고 친숙한 디자인을 제공한다.

## 2-5. 형상관리 & 협업도구
![git](http://img1.daumcdn.net/thumb/R1920x0/?fname=http%3A%2F%2Fcfile21.uf.tistory.com%2Fimage%2F224A234D5905584D369BB9)

git을 사용하여 코드를 관리한다. github를 통해 이슈관리, pull request과 merge commit을 통한 협업을 진행한다.


# 3. 시스템 구성 및 아키텍처
프로젝트는 MVC패턴(Model2) 아키텍쳐를 이용하여 설계, 구축한다. MVC패턴은 시스템을 크게 Model, View, Controller의 세 영역으로 구분하고 영역간의 결합도를 최소화한 패턴이다.

![MVC](http://img1.daumcdn.net/thumb/R1920x0/?fname=http%3A%2F%2Fcfile8.uf.tistory.com%2Fimage%2F257FE74C590558520608F1)

Model 영역은 비즈니스 로직과 사용되는 데이터를 다룬다. 데이터는 데이터베이스에 의해 관리되며, 본 시스템은 오픈소스, NOSQL, 인메모리DB인 Redis를 채택하였다. View 영역은 최종 사용자(올림픽 관광객)에게 보여줄 프리젠테이션 로직을 담당하는 영역이며 JSON형식으로 return해준다. Controller 영역(DispatcherServlet)은 흐름을 관리하며, 모델과 뷰 영역간의 조정역할을 한다. 유저의 요청을 받아 이를 수행하기 위한 비즈니스 로직을 선택하고 호출한다. MVC패턴은 재사용성과 확장이 매우 용이하고 이렇게 하여 “낮은 결합도와 높은 응집도를 구현”할 수 있게 한다.  