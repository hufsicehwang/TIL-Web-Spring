# 🦁TIL-6🦁

## spring IOC container란?
- 일반적으로 처음에 배우는 자바 프로그램에서는 각 객체들이 프로그램의 흐름을 결정하고 각 객체를 직접 생성하고 조작하는 작업(객체를 직접 생성하여 메소드 호출)을 했다.
  - 즉, 모든 작업을 사용자가 제어하는 구조였다. 예를 들어 A 객체에서 B 객체에 있는 메소드를 사용하고 싶으면, B 객체를 직접 A 객체 내에서 생성하고 메소드를 호출한다.
- 하지만 IOC가 적용된 경우, 객체의 생성을 특별한 관리 위임 주체에게 맡긴다. 이 경우 사용자는 객체를 직접 생성하지 않고, 객체의 `생명주기`를 컨트롤하는 주체는 다른 주체가 된다.
  - 즉, 사용자의 제어권을 다른 주체에게 넘기는 것을 `IOC`(제어의 역전) 라고 한다.
> 우리가 기존에 하던 java programming에서는 class마다 class 변수와 함수를 지정하고 이것을 재 사용하기 위해서 다른 class 내부에서 `new` 연산을 통해 직접 객체를 생성 했지만
> spring에서는 객체의 생명주기를 관리하는 주체가 사용자가 아니라 `bean Container` 이다.



![image](https://user-images.githubusercontent.com/67450413/186352353-78ec6cec-8109-470a-9d5f-1509da4b8b96.png)


# Bean이란 
```
Bean이란 IOC container에서 관리하는 자바 객체이다!
```
## Bean을 등록하는 방법
- 1. ` @Component`, `@Configuration-@Bean`, `@Autowired`, `@Service`, `@Repository`, `@Controller` 등의 annotation을 사용
- 2. ApplicationContext.xml 파일에 `<bean id = "example" class = "example" />`와 같이 수동으로 직접 등록

# @Component, @Configuration-@Bean 차이점
### @Component
> 가장 많이 사용하는 bean 객체 등록 annotation으로 개발자가 직접 작성한 Class를 bean으로 등록하고 class에 선언한다.
> >  (value = "") 옵션이 있고, 해당 옵션을 사용하지 않는다면 class의 이름을 camelCase로 변경한 것을 bean id로 사용한다.

### @Configuration-@Bean
> 개발자가 직접 제어가 불가능한 외부 라이브러리 등을 bean으로 등록하고 메소드에만 선언 할 수 있다.
> > __`@Bean`이 선언된 메소드를 가지는 Class는 `@Configuration`을 필수적으로 가져야 한다!__ (`@Configuration-@Bean`는 햄버거-콜라와 같은 세트!!)
> >>  (value = "") 옵션이 있고, 해당 옵션을 사용하지 않는다면 class의 이름을 camelCase로 변경한 것을 bean id로 사용한다.
