---
title: TestTest
description: 
published: true
date: 2023-07-18T01:33:02.929Z
tags: 
editor: markdown
dateCreated: 2023-07-18T01:33:02.929Z
---

# Business Modeler IDE

## **Teamcenter Classes & Business Objects**

### POM이란?
- **POM (Teamcenter persistent object manager)** 은 클래스 및 비즈니스 개체를 사용하여 데이터 모델 아키텍처 또는 스키마를 정의한 Teamcenter 통합 데이터 모델의 최하위 계층
- 대부분의 클래스는 DB 테이블과 유사함.
---
### Class
- 논리적 데이터 모델
- 각 클래스는 이름이 클래스 이름과 동일한 기본 비즈니스 개체를 가지고 있음.
- 기본 개체는 **POM_object**
- 일반적으로 상위와 하위 클래스는 **UID (Unique Identify)** 로 연결되어 있음.
	
	![95ed07_44408671190d49f2b1f3c54838b416a6~mv2.webp](/95ed07_44408671190d49f2b1f3c54838b416a6~mv2.webp)
---
- 클래스 계층
	
	![95ed07_6ff73d7ee4974fe8a9795d81486f3ab7~mv2.webp](/95ed07_6ff73d7ee4974fe8a9795d81486f3ab7~mv2.webp)

---

### Business Object
- Teamcenter 통합 비즈니스 및 해당 프로세스에 대한 실제 엔티티를 나타내고 사용자가 클라이언트에서 작업하는 객체.
- **persistence (영속성)** 또는 **non-persistence (compound , runtime , typedReference ...)** 속성이 있음.
- **relation 객체**를 통해 각 비즈니스 객체끼리 연결됨.
- Naming Rule , condition , extensions , GRM (Generic Relationship Management) Rule , display Rule , deep copy rule 등 여러 규칙으로 제어되고 관리됨.
- 상속을 지원하며 **상위 Business 객체에 정의된 모든 속성**들은 하위 Business 객체에 **상속**이 됨.
	
	![95ed07_607f79f84e1f46578b0600f2d0b9fa87~mv2.webp](/95ed07_607f79f84e1f46578b0600f2d0b9fa87~mv2.webp)
---

















[BMIDE 공식 문서]: https://docs.sw.siemens.com/en-US/doc/282219420/PL20210421143201885.plm00071/xid366843