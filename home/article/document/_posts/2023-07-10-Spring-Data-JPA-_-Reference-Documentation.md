---
layout: article
---

> [Spring Data JPA - Reference Documentation](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/)

> Oliver Gierke, Thomas Darimont, Christoph Strobl, Mark Paluch, Jay Bryant, Greg Turnquist
>
> Version 3.1.1
>
> 2023-06-16
> 
> © 2008-2023 The original authors.

> Copies of this document may be made for your own use and for distribution to others, provided that you do not charge any fee for such copies and further provided that each copy contains this Copyright Notice, whether distributed in print or electronically.

---

**index**
1. Preface
2. Upgrading Spring Data
3. Dependencies
4. Working with Spring Data Repositories
5. Reference Documentation
6. Appendix
7. Appendix A : Namespace reference
8. Appendix B : Populators namespace reference
9. Appendix C : Repository query keywords
10. Appendix D : Repository query return types
11. Appendix E : Frequently Asked Questions
12. Appendix F : Glossary

---

# 1. 머리말

Spring Data JPA는 Jakarta Persistence API(JPA)에 대한 리포지토리 지원을 제공한다. 이는 JPA 데이터 소스에 액세스해야 하는 애플리케이션
개발을 용이하게 한다.

## 1.1. Project Metadata

- Version control: https://github.com/spring-projects/spring-data-jpa
- Bugtracker: https://github.com/spring-projects/spring-data-jpa/issues
- Milestone repository: https://repo.spring.io/milestone
- Snapshot repository: https://repo.spring.io/snapshot

# 2. Spring Data 업그레이드

이전 버전의 Spring Data에서 업그레이드하는 방법에 대한 지침은
[프로젝트 위키](https://github.com/spring-projects/spring-data-commons/wiki)에서 제공된다.

업그레이드 지침은 항상 release 정보의 첫 번째 항목이다. 두 개 이상의 release가 뒤쳐진 경우 점프한 버전의 release 정보도 검토해야 한다.

# 3. 의존성

개별 스프링 데이터 모듈의 시작 날짜가 다르기 때문에 대부분은 서로 다른 주 버전 번호와 부 버전 번호를 가지고 있다. 호환 가능한 버전을 찾는 가장 쉬운 방법은
정의된 호환 버전과 함께 제공되는 Spring Data Release Train BOM에 의존하는 것이다. Maven 프로젝트에서는 다음과 같이 POM의
`<dependencyManagement \>` 섹션에서 이 의존성을 선언한다.

```xml
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>org.springframework.data</groupId>
      <artifactId>spring-data-bom</artifactId>
      <version>2023.0.1</version>
      <scope>import</scope>
      <type>pom</type>
    </dependency>
  </dependencies>
</dependencyManagement>
```

현재 release 트레인 버전은 `2023.0.1`이다. 트레인 버전은 `YYYY.MINOR.MICRO` 패턴의 `${calver}`를 사용한다. 버전 이름은 GA release 및
서비스 release의 경우 `${calver}`를 따르고 다른 모든 버전의 경우 `${calver}-${modifier}` 패턴을 따른다. 여기서 수정자는 다음 중 하나일 수 있다.

- `SNAPSHOT` : Current snapshots
- `M1`, `M2` and so on : Milestones
- `RC1`, `RC2` : Release candidates

[Spring Data 예제 리포지토리](https://github.com/spring-projects/spring-data-examples/tree/main/bom)에서 BOM을 사용하는 작업 예제를
찾을 수 있다. 이를 통해 다음과 같이 `<denpendencies \>` 블록에서 버전 없이 사용하려는 Spring Data 모듈을 선언할 수 있다.

```xml
<dependencies>
  <dependency>
    <groupId>org.springframework.data</groupId>
    <artifactId>spring-data-jpa</artifactId>
  </dependency>
<dependencies>
```

## 3.1. Spring Boot의 의존성 관리

Spring Boot는 최신 버전의 Spring Data 모듈을 선택한다. 자세한 내용은 [Spring Boot's documentation](https://docs.spring.io/spring-boot/docs/current/reference/html/dependency-versions.html#appendix.dependency-versions.properties)(search for "Spring Data Bom")을
참조하라.

## 3.2. Spring Framework

Spring 데이터 모듈의 현재 버전에는 Spring Framework 6.0.10 이상이 필요하다. 모듈은 해당 마이너 버전의 이전 버그 수정 버전에서도 작동할 수 있다.
그러나 해당 세대 내에서 가장 최신 버전을 사용하는 것이 좋다.

