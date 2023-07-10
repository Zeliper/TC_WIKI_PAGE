---
title: Test Document 1
description: 
published: true
date: 2023-07-10T04:26:58.082Z
tags: 
editor: markdown
dateCreated: 2023-07-10T03:52:23.702Z
---

# Header
Your content here

## 예제 1

- OOTB 모듈을 활용한 Object 및 Property 로드

```js
let obj = clientDataModel.getObject(uid); // uid를 이용해 ModelObject를 가져옴.

clientDataModel.getProperty(obj , "object_name"); // ModelObject가 가지고 있는 속성.

console.log(obj);
``` 

## 예제 2 

Tempermonkey에 미리 정의한 함수 활용

```js
let obj = getObj(uid); // arr 지원

getProps(uids , props); // uid arr 와 obj arr 지원

console.log(obj);
```