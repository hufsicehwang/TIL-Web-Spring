# 🦈TIL-4🦈

# Service
- Repository에서 작성한 DAO를 이용해서 database의 data에 접근해서 수행 할 transacion을 작성 한다.
```java
public class MemberService {
    private final MemberRepository memberRepository;
    public MemberService(MemberRepository memberRepository) {
        this.memberRepository = memberRepository;
    }

    @Transactional
    public int join(Member member) {

        memberRepository.save(member);
        return member.getId();
    }
    @Transactional
    public List<Member> findMembers() {

        return memberRepository.findAll();
    }
    @Transactional
    public Optional<Member> findOne(int memberId) {

        return memberRepository.findById(memberId);
    }
}
```
> `@transactional` 어노테이션을 사용해서 해당 메소드가 transaction이 되도록 보장해 준다.
>>  Spring은 해당 메서드에 대한 프록시를 만든다. 프록시 패턴은 디자인 패턴 중 하나로, 어떤 코드를 감싸면서 추가적인 연산을 수행하도록 강제하는 방법이다. 
>>>  트랜잭션의 경우, 트랜잭션의 시작과 연산 종료시의 커밋 과정이 필요하므로, 프록시를 생성해 해당 메서드의 앞뒤에 트랜잭션의 시작과 끝을 추가하는 것이다.

# Controller
- 사용자와 의사소통 할 수 있는 point이다.
- View에서 요청 받은 것을 어떤 Service로 매핑 시킬 것 인가를 정한다.
- Service에서 처리한 결과를 View로 응답하여 보여 준다.
  - API를 작성한다. 
```java
@Controller
public class MemberController {

    private final MemberService memberService;

    @Autowired
    public MemberController(MemberService memberService) {
        this.memberService = memberService;
    }

    @GetMapping("/members/new")
    public String createForm() {

        return "members/createMemberForm";
    }

    @PostMapping("/members/new")
    public String create(MemberForm form) {
        Member member = new Member();
        member.setName(form.getName());
        member.setTeam(form.getTeam());
        member.setTitle(form.getTitle());
        member.setText(form.getMessage());
        member.setRegisterTime(LocalDateTime.now());

        memberService.join(member);

        return "redirect:/members";
    }

}
```
> `get`, `post`, `put`, `patch`, `delete`에 대해서 mapping 한다.
> > 특정한 request에 대해서 올바른 Service를 선택한다.

## @Autowired
- 스프링 DI(Dependency Injection)에서 사용되는 어노테이션
- 스프링에서 빈 인스턴스가 생성된 이후 @Autowired를 설정한 메서드가 자동으로 호출되고, 인스턴스가 자동으로 주입
- 해당 변수 및 메서드에 스프링이 관리하는 Bean을 자동으로 매핑해주는 개념

### DI(Dependency Injection)란
- DI(의존성 종속, Dependency Injection)란, 클래스간의 의존관계를 스프링 컨테이너가 자동으로 연결해주는 것

### DI가 필요한 이유
![image](https://user-images.githubusercontent.com/67450413/184641438-917ae46f-fc52-47dc-a244-11dd39a51256.png)
- SW를 사용하는 고객은 Factory 클래스만을 호출해야하며, 그것이 ConsoleFactory인지 UserFactory인지 몰라야 함
- 고객마다 전용 Factory를 생성할 경우 코드 생산성이 떨어지며, 고객이 몰라도 되는 코드가 노출 됨
- 때문에 스프링은 Factory가 ConsoleFactory인지 UserFactory인지를 프레임워크가 자동으로 객체간 의존성을 주입
