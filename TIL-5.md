# 🐱TIL-5🐱

## YAML이란
- 데이터 표현 양식의 한 종류
- 우리가 일반적으로 사용하는 JSON, XML 보다도 더욱 인간이 보고 이해하기 쉬운 형태
- YAML, YLM이라고 표기하며 보통`야믈`이라고 발음 한다.

### YAML 포멧
```yaml
#YAML
Servers:
  - name: Server1
    administrator: Kim
    created: 20050103132749
    status: active
  - name: Server2
    administrator: Lee
    created: 20210101000000
    status: active
```
### JSON 포멧
```xml
#JSON
{
  Servers:[
    {
      name: Server1,
      administrator: Kim,
      created: 20050103132749,
      status: active
    },
    {
      name: Server2,
      administrator: Lee,
      created: 20210101000000,
      status: active
    }
  ]
}
```
### XML 포멧
```xml
#XML
<servers>
  <entry>
    <name>server1</name>
    <administrator>kim</administrator>
    <created>20050103132749</created>
    <status>active</status>
  </entry>
  <entry>
    <name>server2</name>
    <administrator>Lee</administrator>
    <created>20210101000000</created>
    <status>active</status>
  
  </entry>
</servers>
```

## YAML 사용방법
- key-value로 데이터 정의
- 들여쓰기는 기본적으로 2칸, 4칸 사용
- 여러 데이터를 배열요소로 표현시 시작부분에 `-` 기호 삽입
- 주석은 `#` 사용
- https://yaml.org/   공식 reference

# YAML 사용하기
## 1.YAML로 file 경로 지정하기
- `resource` directory 내부에 application.yml을 작성한다.
```yaml
tools:
  log-path:
    base: C:\Users\User\Desktop\log
    dags1: C:\Users\User\Desktop\log\dags1
    dags2: C:\Users\User\Desktop\log\dags2
    dems1: C:\Users\User\Desktop\log\dems1\trace
    dems2: C:\Users\User\Desktop\log\dems2\trace
```

## 2.Component 지정
- `component` 패키지 생성 후 `ToolProperties.java` 작성
```java
@Component
@Getter
public class ToolProperties {
    @Value("${tools.log-path.base}")
    private String logBasePath;

    @Value("${tools.log-path.dags1}")
    private String dags1LogPath;

    @Value("${tools.log-path.dags2}")
    private String dags2LogPath;

    @Value("${tools.log-path.dems1}")
    private String dems1LogPath;

    @Value("${tools.log-path.dems2}")
    private String dems2LogPath;
}
```
> class 변수에 `@Value` 어노테이션을 사용해서 할당
> > `@Component` 어노테이션을 사용해서 Bean Configuration 파일에 Bean을 따로 등록하지 않고도 빌드시 bean 객체 자동 등록
> > > 추후 사용하고자 하는 부부에서 class 변수를 이용해 getter method로 사용
