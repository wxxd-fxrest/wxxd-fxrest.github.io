---
title: MySQL과 MongoDB의 차이점
date: 2024-09-06 20:04:00 +09:00
categories: [데이터베이스(Database), SQL(Structured Query Language)]
tags:
  [
    MySQL,
    MongoDB,
    관계형 데이터베이스,
    비관계형 데이터베이스,
    SQL,
    NoSQL,
  ]
---

<br/>
<br/>

# MySQL과 MongoDB의 차이점
데이터베이스 관리 시스템(DBMS)은 애플리케이션의 데이터 저장 및 관리를 위한 핵심 요소이다. **MySQL과 MongoDB는 각각 관계형 데이터베이스와 비관계형 데이터베이스의 대표적인 예**인데, 두 시스템의 주요 차이점과 각각의 장단점을 살펴보자.  

<br/>

## 1. 데이터 저장 방식
### MySQL
- **관계형 데이터베이스**: MySQL은 관계형 데이터베이스 관리 시스템(RDBMS)으로, <span style="color: #0550ae; font-weight: bold">데이터를 테이블 형태로 저장</span>한다. 각 테이블은 행(Row)과 열(Column)로 구성되어 있으며, 스키마가 고정되어 있다.
- **정형 데이터**: 데이터가 구조화되어 있어, <span style="color: #0550ae; font-weight: bold">사전에 정의된 스키마에 따라 데이터를 저장</span>해야 한다.  

<br/>

### MongoDB
- **비관계형 데이터베이스**: MongoDB는 NoSQL 데이터베이스로, **JSON과 유사한 BSON 형식으로 데이터를 저장**한다. 데이터는 문서(Document) 형태로 저장되며, 스키마가 유연하다.
- **비정형 데이터**: 데이터 구조가 유동적이어서, 서로 다른 형식의 데이터를 같은 컬렉션(Collection)에 저장할 수 있다.

<br/>
* * *
<br/>

## 2. 쿼리 언어
### MySQL
- **SQL 사용**: MySQL은 **Structured Query Language(SQL)를 사용하여 데이터를 조회하고 저장**한다. SQL은 강력한 쿼리 언어로, 복잡한 조인(JOIN)과 서브쿼리를 지원한다.  

<br/>

### MongoDB
- **MongoDB 쿼리 언어**: MongoDB는 **JavaScript 기반의 쿼리 언어를 사용하여 데이터를 조회**한다. 문서 기반의 쿼리를 통해 필드 값에 따라 데이터를 쉽게 검색할 수 있으며, 집계 프레임워크를 통해 복잡한 데이터 분석이 가능하다.  

<br/>
* * *
<br/>

## 3. 트랜잭션 처리
### MySQL
- **ACID 준수**: MySQL은 ACID(Atomicity, Consistency, Isolation, Durability) 속성을 준수하여 데이터의 무결성과 일관성을 보장한다. 이는 금융 시스템과 같이 데이터 무결성이 중요한 환경에 적합하다.  

<br/>

### MongoDB
- **비ACID 지원**: MongoDB는 기본적으로 ACID 트랜잭션을 지원하지 않지만, 4.0 버전 이후로 다중 문서 트랜잭션을 지원하게 한다. 그러나 여전히 MySQL에 비해 트랜잭션 처리의 강력함이 떨어질 수 있다.  

<br/>
* * *
<br/>

## 4. 확장성
### MySQL
- **수직적 확장**: MySQL은 수직적 확장(Vertical Scaling)이 일반적이다. 즉, 서버의 성능을 높이는 방향으로 확장하게 됩니다. 이는 하드웨어의 한계에 부딪힐 수 있다.  

<br/>

### MongoDB
- **수평적 확장**: MongoDB는 수평적 확장(Horizontal Scaling)을 지원하여, 데이터베이스 서버를 추가하여 데이터베이스의 용량과 성능을 확장할 수 있다. 이는 대규모 데이터 처리에 유리하다.  

<br/>
* * *
<br/>

## 5. 사용 사례
### MySQL
- **전통적인 웹 애플리케이션**: MySQL은 구조화된 데이터가 필요한 전통적인 웹 애플리케이션, 금융 시스템, ERP 시스템 등에서 많이 사용된다.  

<br/>

### MongoDB
- **대규모 데이터 처리**: MongoDB는 소셜 미디어, IoT, 실시간 데이터 분석 등 비정형 데이터가 많이 발생하는 환경에서 유리하다.  

<br/>

결론적으로 MySQL과 MongoDB는 각기 다른 장단점을 가지고 있으며, 사용자의 필요에 따라 적합한 데이터베이스를 선택하는 것이 중요하다. 정형 데이터 및 복잡한 쿼리가 필요한 경우 MySQL이 적합하고, 비정형 데이터 및 대규모 데이터 처리에 유리한 경우 MongoDB를 고려할 수 있다.






