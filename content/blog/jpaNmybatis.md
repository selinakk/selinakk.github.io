---
title: Java 데이터베이스 연동 기술 JPA vs MyBatis 이해하기
description: 자바 데이터베이스를 연동하는 ORM(JPA+Hibernate) 방식과 SQL 매퍼 방식(MyBatis) 개념
date: 2024-11-10
tags: Backend
---

<br/>

Java 데이터베이스 연동 기술들에 대해 알아봅시다<br/>
기본 개념인 JDBC(Java Database Connectivity)부터 살펴봅니다<br/><br/>
 

## 1. JDBC
**자바에서 데이터베이스와 통신하기 위한 기본 API**<br/>
SQL 쿼리를 직접 작성하고, 연결/실행/결과 처리를 직접 구현해야 함<br/>
<br/>

## 2. ORM 방식: JPA + Hibernate
**JPA**는 자바의 ORM **(Object Relational Mapping) 표준**이며, **Hibernate**는 그 표준을 구현한 **ORM 프레임워크**
<br/>

### 2-1. JPA(Java Persistence API)
Java의 표준 ORM API로 자바 객체와 데이터베이스 간의 상호작용을 관리하는 표준을 정의합니다<br/>
**JPA 자체는 인터페이스와 표준 스펙만 제공**하므로 실제 구현체(Hibernate, EclipseLink 등)가 필요합니다<br/>
JPA는 SQL을 직접 작성하지 않고, Entity(엔티티)라는 자바 객체를 통해 데이터베이스를 다룹니다 => 필요한 **쿼리를 자동으로 생성하고 실행**합니다<br/>
유지보수가 용이하고 코드가 간결해지는 장점이 있습니다<br/>
하지만 복잡한 쿼리 사용이 어렵고 활용 난이도가 있어 진입장벽이 높습니다
<br/><br/>

_🙋🏻‍♀️ 잠깐_
<br/>
**Object Relational Mapping**이 뭔데?<br/>
객체 지향 언어인 **자바의 객체와 관계형 데이터베이스의 테이블을 자동으로 매핑**하는 기술입니다<br/>
JPA에서는 데이터베이스의 테이블을 Entity 클래스라는 자바 클래스로 표현하고, 이 클래스는 데이터베이스 테이블과 일대일로 매핑됩니다<br/><br/>

_🙋🏻‍♀️ 잠깐_
<br/>
**Persistence**란?<br/>
영속성입니다. **데이터를 데이터베이스에 영구적으로 저장하고 관리하는 개념**입니다<br/>
자바 객체와 데이터베이스 간의 동기화를 관리하는 역할을 합니다<br/>
JPA든 MyBatis든 모두 데이터를 영속화 하기 위한 기술인 셈입니다 접근 방식이 다른 거죠<br/><br/>

### 2-2. Hibernate
**Hibernate는 JPA의 실제 구현체**입니다. JPA에서 정의한 표준을 따르며 추가적인 기능을 제공하는 **ORM 프레임워크**입니다<br/>
Hibernate의 독자적인 기능도 제공하기 때문에 유연성과 확장성이 있습니다<br/>


### 2-3. Spring Data JPA
Spiring Data JPA는 JPA와 Hibernate를 더욱 간편하고 효율적으로 사용할 수 있게 돕는 Spring의 라이브러리입니다<br/>
**JPA + Hibernate는 기본적인 ORM 기능만 제공하는 반면 Spring Data JPA는 자동 구현 기능을 제공**합니다<br/>
Spring Data JPA의 Repository 인터페이스를 통해 데이터를 쉽게 관리할 수 있게 합니다<br/>
@Query 어노테이션을 사용하여 커스텀 쿼리를 사용할 수 있습니다<br/><br/>

## 3. SQL Mapper 방식: MyBatis
마이바티스는 JDBC 기반의 **SQL 매퍼 프레임워크**입니다<br/>
JDBC를 쉽고 간편하게 사용하기 위한 상위 레이어의 프레임워크로, **코드와 SQL의 분리 및 자동 매핑 기능을 제공**합니다<br/>
SQL을 XML파일로 분리해 쿼리를 깔끔하게 분리할 수 있습니다<br/>
SQL을 제어하기 쉽고 복잡한 쿼리에도 유리하지만, SQL을 직접 작성해야 하므로 JPA보다 코드가 길어질 수 있습니다<br/>
또한 수동으로 SQL을 작성해야 하기 때문에 불필요한 반복 작업이 필요할 수 있습니다<br/><br/>

_🙋🏻‍♀️ 잠깐_
<br/>
**SQL 매핑이 뭔데?**<br/>
SQL 쿼리와 자바 객체의 명시적으로 연결하는 작업(mapping)입니다
<br/><br/>
 

_🙋🏻‍♀️ 잠깐_
<br/>
**복잡한 쿼리 기준이 뭔데!**<br/>
- 여러 테이블 조인
- 서브 쿼리(쿼리 안에 또 다른 쿼리)
- 대량 데이터 처리
- WHERE절에서 다양한 조건

<br/>
만약 혼용을 하게 된다면 간단한 CRUD 작업은 JPA를 사용하고, 복잡한 쿼리 필요시에만 MyBatis를 사용하는 게 좋습니다<br/><br/>

## 4. 기타 방식: NoSQL 등
NoSQL (MongoDB, Cassandra 등)은 관계형 데이터베이스 대신 사용할 수 있는 데이터베이스 시스템입니다<br/>
관계형 DB의 제약에서 벗어난 방식으로 데이터를 처리할 수 있습니다