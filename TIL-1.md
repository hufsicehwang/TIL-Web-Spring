# 🐳TIL-1🐳

## 1. 프로젝트 생성 부터 실행
1. IntelliJ 또는 Eclipse 설치
2. JDK는 11 버전으로 설치하는게 오류날 확률 적음
3. https://start.spring.io/ 에서 스프링 프로젝트 생성
    - Project: Gradle Project
    - Spring Boot: 2.3.x
    - Java: 11
    - __Dependencies: Spring Web, Thymeleaf__
4. IntelliJ로 Open
5. (프로젝트명)Aplication.java 내부의 메인 메소드 Run
6. `http://localhost:8080/`에서 확인

## 2. MVC 모델
![image](https://user-images.githubusercontent.com/67450413/181166692-6f9a976d-0e70-4785-ac21-9b4800ecaff7.png)
- Model : 데이터페이스와 연동하여 사용자가 입력한 데이터나 사용자에게 출력할 데이터를 다룸
  - domain, repository, service에 해당됨
- View : 모델이 처리한 데이터나 그 작업 결과를 가지고 사용자에게 출력할 화면을 만듬
  - html로 구성된 thymeleaf(template engine)에 해당됨 
- Controller : client 측에서 request했을때 response 해줄 함수를 mapping 해줌
  - controller.java에 해당됨

##  3. Spring Boot 내부 요소
### gradle
> Ant와 Maven과 같은 이전 세대 빌드 도구의 단점을 보완하고 장점을 취합하여 만든 오픈소스 `빌드 도구`
### /sql/ddl.sql
> 연동된 데이터베이스에 실행할 수 있는 SQL Data Definition Language
### /src/main/resource/application.properties
> 데이터베이스 연결 설정 추가
>> 스프링부트 2.4부터는 `spring.datasource.username`를 꼭 추가 해야함.
### /src/main/java/프로젝트/domain/Member.java
> 모델 계층인 domain에서 `Entity`에 해당 
### /src/main/java/프로젝트/domain/MemberForm.java
> 모델 계층인 domain에서 `DTO(Data Transfer Object)`에 해당
### /src/main/java/프로젝트/repository/MemberRepository.java
> DAO를 작성할 추상부를 정의한 인터페이스
### /src/main/java/프로젝트/repository/JpaMemberRepository.java
> DAO를 JPA를 통해서 작성
### /src/main/java/프로젝트/service/MemberService.java
> __`Repository`에서 JPA를 이용해서 작성한 DAO의 transaction을 생성__
