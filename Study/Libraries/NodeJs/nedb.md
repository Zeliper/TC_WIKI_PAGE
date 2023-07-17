---
title: nedb
description: Node.js의 파일 베이스 데이터베이스 시스템
published: true
date: 2023-07-17T14:56:42.351Z
tags: 
editor: markdown
dateCreated: 2023-07-17T14:50:18.450Z
---

# nedb
고양이가 귀여운 파일 베이스의 데이터베이스
DB에 값을 쓰면 Json 형식으로 저장된다.

[공식 Github 주소](https://github.com/louischatriot/nedb)

## 설치법

nedb를 설치할 폴더에서 CMD창에 다음 명령어 입력하여 설치

```npm
npm install nedb --save
```

## 사용법

상세 가이드는 공식 문서 참고

[공식 Github 주소](https://github.com/louischatriot/nedb)

### DB Initialize

데이터 베이스 초기화 예시

```js
var Datastore = require('nedb') //nedb Class 로드
  , db = new Datastore(); //db 변수에 Datasotre 클래스 생성
  
db.posts = new Datastore('posts.db'); //posts.db에 db.posts 테이블 데이터 링크
db.comments = new Datastore('comments.db'); //comments.db에 comments.posts 테이블 데이터 링크

//데이터 베이스 로드
db.posts.loadDatabase();
db.comments.loadDatabase();
```

### DB Insert
데이터 베이스 값 입력 예시
```js
let doc = {
  title : "Test Data"
}

//posts DB에 값을 입력하는 예시
db.posts.insert(doc, (err, newPost) => {
  // err 			- 에러처리를 위한 변수
  // newPost 	- 생성된 Document Json데이터
});
```

### DB Clear
데이터 베이스 초기화 예시
```js
//posts DB의 모든 데이터를 삭제하는 예시
// multi : true로 지정할 경우 전체 삭제, false일 경우 한개씩 삭제됨
db.posts.remove({}, { multi: true }, function (err, numRemoved) {
  // err 				- 에러처리를 위한 변수
  // numRemoved - 지워진 문서 개수
});
```
