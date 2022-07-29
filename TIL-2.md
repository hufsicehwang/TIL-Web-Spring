# 🦄TIL-2🦄
## Spring Boot 전형적인 package 구조
- Controller
- DTO
- Service
- Repository
- Domain (Entity)
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FC7HSi%2FbtrtYU5BG4N%2FuaTJCaFk9ikMg4JkalvU71%2Fimg.png"></img>

## 1. Domain
- DB 테이블과 직접 맵핑되는 클래스로서 JPA 사용 시 어노테이션을 이용하여 테이블, 필드, 등을 설정한다.
- domain과 client를 직접 연결하지 않고 DTO를 이용해서 분리한다.
  -  Client 쪽과 연결된 부분은 잦은 변경사항이 있을 수 있는데 Domain과 연결되어 자주 변경되게 된다면 여러 클래스에 영향을 미치기 때문에 분리한다.
  -  View 단과 DB 단을 확실하게 분리하여 관리한다.
```java
  package hello.hellospring.domain;
import javax.persistence.Entity;

@Entity
public class Member {
    private String title;
    private String text;

    }
    public String getTitle() {
        return title;
    }
    public void setTitle(String title) {
        this.title = title;
    }

    public String getText() {
        return text;
    }
    public void setText(String text) {
        this.text = text;
    }
}
```
> 기본적인 어노테이션 : @Entity
> > DB table에 포함되는 attribute들을 가진다.
> > > setter와 getter를 설정한다. (`ALT`+`insert`키로 자동 생성 가능)

## 2. DTO
- Data Transfer Object로 "데이터 전송 객체"이다.
- Domain은 DB 테이블에 대한 정보를 가지고 있는 클래스이고, DTO는 해당 테이블에서 실제로 CRUD를 할 필드를 정의해둔 것 이다.
```java
package hello.hellospring.domain;

public class MemberForm {
    private String title;
    private String message;

    public String getTitle() {
        return title;
    }
    public void setTitle(String title) {
        this.title = title;
    }

    public String getMessage() {
        return message;
    }
    public void setMessage(String message) {
        this.message = message;
    }
}

```
> 기본적인 어노테이션 : 없음
> > 쉡게 생각해 client 측에서 입력 받아 POST 요청 올 데이터에 해당한다.
> > > setter와 getter를 설정한다. (`ALT`+`insert`키로 자동 생성 가능)
