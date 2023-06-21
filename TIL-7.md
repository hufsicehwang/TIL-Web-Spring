# Maven
- 아파치 메이븐
- 자바 전용 / 아파치 Ant의 대안
- 연관 된 라이브러리 관리 지원

## POM(Project Object Model)
- xml 형태
- 프로젝트 정보, 빌드 설정, 빌드 환경, POM 연관 정보(의존성, 상위-하위 프로젝트/모듈)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.5.2</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
    <groupId>com.example2</groupId>
    <artifactId>demo-maven</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <name>demo-maven</name>
    <description>Demo project for Spring Boot</description>
    <properties>
        <java.version>11</java.version>
    </properties>
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter</artifactId>
        </dependency>
 
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>
 
    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
 
</project>
```



# Gradle
- 그레이들
- Java, C/C++, Python 지원 / 기존 Ant 빌드툴과 Groovy 스크립트 기반
- 메이븐 보다 빠름

```gradle
plugins {
    id 'org.springframework.boot' version '2.5.2'
    id 'io.spring.dependency-management' version '1.0.11.RELEASE'
    id 'java'
}
 
group = 'com.example'
version = '0.0.1-SNAPSHOT'
sourceCompatibility = '11'
 
repositories {
    mavenCentral()
}
 
dependencies {
    implementation 'org.springframework.boot:spring-boot-starter'
    testImplementation 'org.springframework.boot:spring-boot-starter-test'
}
 
test {
    useJUnitPlatform()
}
```

# Maven과 Gradle의 차이점
- 스크립트 길이와 가독성 면에서 gradle이 우세하다.
- gradle은 캐시를 사용하기 때문에 빌드와 테스트 반복시 우세할 뿐만 아니라 기존 빌드 및 테스트 속도도 gradle이 더 빠르다. 


