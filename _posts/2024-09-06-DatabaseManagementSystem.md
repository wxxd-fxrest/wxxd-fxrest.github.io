---
title: 데이터베이스(Database)와 DBMS(Database Management System)란?
date: 2024-09-06 20:20:00 +09:00
categories: [데이터베이스(Database), DBMS(Database Management System)]
tags:
  [
    Database,
    DBMS,
    MySQL,
    DatabaseManagementSystem,
    RDBMS,
  ]
---

<br/>
<br/>

# 데이터베이스(Database)와 DBMS(Database Management System)에 대한 이해

## 데이터베이스(Database)란?
데이터베이스(Database)는 정보를 저장하고 관리하는 <span style="color: #0550ae; font-weight: bold">데이터의 집합체</span>이다. 우리의 일상에서 발생하는 다양한 정보, 하다못해 오늘 내가 보내고 받은 메시지나 블로그 글을 작성하고 업로드하는 것조차 데이터베이스(Database)에 기록된다.  

예를 들어, 학교에서는 학생들의 성적, 정보 등을 서버에 데이터로 저장하고 이를 학교 사이트, 학생 앱, 가정 통신문, 대학 내신 제출 시 등에 활용한다. 이러한 방식으로 원하는 곳에서 데이터만 저장되어 있다면 언제든지 접근하여 사용할 수 있다.  

또한, 데이터베이스(Database)는 특정 소프트웨어나 프로그램에 종속되지 않는 **독립된 데이터의 집합체 또는 저장소**이다.   

<br/>
* * *
<br/>

## DBMS(Database Management System)란?
DBMS(Database Management System)(데이터베이스 관리 시스템)는 데이터베이스를 관리하고 운영하는 소프트웨어이다. 다양한 데이터가 저장된 데이터베이스는 다수의 사용자 또는 응용 프로그램과 공유되고 동시에 접근 가능해야 한다.  

<br/>
<br/>

### DBMS(Database Management System)의 특징

| **DBMS**        | **제작사**   | **작동 운영체제**                    | **기타**                             |
|------------------|---------------|--------------------------------------|--------------------------------------|
| MySQL            | Oracle        | Unix, Linux, Windows, Mac            | 오픈 소스(무료), 상용                |
| MariaDB         | MariaDB       | Unix, Linux, Windows                 | 오픈 소스(무료), MySQL 초기 개발자들이 독립하여 개발 |
| PostgreSQL      | PostgreSQL    | Unix, Linux, Windows, Mac            | 오픈 소스(무료)                      |
| Oracle           | Oracle        | Unix, Linux, Windows                 | 상용 시장 점유율 1위                 |
| SQL Server       | Microsoft     | Windows                              | 주로 중/대형급 시장에서 사용         |
| DB2              | IBM           | Unix, Linux, Windows                 | 메인프레임 시장 점유율 1위           |
| Access           | Microsoft     | Windows                              | PC용                                 |
| SQLite           | SQLite        | Android, iOS                         | 모바일 전용, 오픈 소스(무료)         |


<br/>
<br/>

### DBMS(Database Management System)의 분류
DBMS의 유형은 다음과 같이 분류된다:
- **계층형(Hierarchical)**
- **망형(Network)**
- <span style="color: #0550ae; font-weight: bold">관계형(Relational)</span>
- **객체지향형(Object-Oriented)**
- **객체관계형(Object-Relational)**
현재 사용되는 DBMS 중 관계형 DBMS가 가장 많은 부분을 차지하며, <span style="color: #0550ae; font-weight: bold">MySQL도 이 관계형 DBMS(RDBMS)에 포함</span>된다.  

<br/>
* * *
<br/>


## 데이터베이스 (Database) & DBMS (Database Management System) 요약
### 데이터베이스 (Database)
- **정의**: 정보를 저장하는 데이터의 집합체.
- **특징**:
  - 구조화된 데이터 저장.
  - 다양한 형식의 데이터(예: 텍스트, 이미지 등)를 포함.
  - 데이터의 검색, 관리, 처리 가능.  
  
### DBMS (Database Management System)
- **정의**: 데이터베이스를 관리하고 운영하는 소프트웨어.
- **기능**:
  - 데이터 생성, 읽기, 업데이트, 삭제(CRUD) 기능 제공.
  - 데이터 무결성, 보안 및 효율성 유지.
  - 다수의 사용자가 동시에 데이터베이스에 접근 가능하게 지원.  


데이터베이스는 데이터의 집합체이고, DBMS는 그 데이터를 관리하는 시스템이다. 이 둘은 함께 작동하며 효율적으로 데이터 저장 및 관리할 수 있다. 

<br/>
<br/>
<br/>
* * *
<br/>
<br/>
<br/>

> **Reference**  
1. <a href="https://www.youtube.com/watch?v=dgpBXNa9vJc" style="text-decoration: none; color: #757575;">갖고 노는 MySQL 데이터베이스 강좌</a>
2. <a href="https://hongong.hanbit.co.kr/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-databasedb-dbms-sql%EC%9D%98-%EA%B0%9C%EB%85%90/" style="text-decoration-line: none; color: #757575;">데이터베이스 이해하기</a>