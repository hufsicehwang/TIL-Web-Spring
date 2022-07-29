# 🐲TIL-3🐲

## 1. Repository
- 데이터베이스에 접근하여 CRUD의 연산을 할 JPA에 대해서 작성하는 부분이다.
- 인터페이스의 추상부와 implements 하는 구현부로 나누어져 있다.
```java
public interface MemberRepository {
    Member save(Member member);
    Optional<Member> findById(int Id);
    List<Member> findAll();
}v
```
> __DataBase CRUD 연산 생성!__
> > optional을 사용하는 이유는 NPE(NullPointException)을 피하기 위함이다. (특정 tupple을 찾는 Read 연산은 찾아보고 없으면 NULL을 반환하기 때문에 optional을 사용)

```java

public class JpaMemberRepository implements MemberRepository {

    private final EntityManager em;
    public JpaMemberRepository(EntityManager em) {
        this.em = em;
    }

    @Override
    public Member save(Member member) {
        em.persist(member);
        return member;
    }

    @Override
    public Optional<Member> findById(int Id) {
        Member member = em.find(Member.class, Id);
        return Optional.ofNullable(member);
    }

    @Override
    public List<Member> findAll() {
        return em.createQuery("select m from Member m", Member.class)
                .getResultList();
    }
}

```
> `JPA` 작성을 위해 `EntityManager`를 사용한다!!!
> > EntityManager 내장 함수 `createQuery` : SQL 작성, `persist` : entity에 영속성을 부여, `find` : 즉시로딩 방식으로 `PK`를 활용하여 __하나의 객체를 매핑!!!__
> > > `지연로딩` : JDBC 같은 느낌 인 것 같음(느림, 코드김), `즉시로딩` : EntityManager의 내장 함수를 사용해서 객체를 빠르게 매핑
