---
title: 000.React로 게시판 만들기
description: 
published: true
date: 2023-07-17T15:40:48.935Z
tags: 
editor: markdown
dateCreated: 2023-07-17T14:18:57.278Z
---

# React로 게시판 만들기

## Git Repository (소스 포함)

Private Git 레포지토리 : [Zeliper/notice-board](https://github.com/Zeliper/notice-board)

## 준비물

[Node.js 16 이상](/ko/Study/Libraries/NodeJs) - 대충 LTS 버전인 18.16.1 설치 하면 된다. (설치시 Add To PATH 가 체크되어있는지 꼭 확인할것)

Database 둘중 택1
- Node.js의 [nedb](/ko/Study/Libraries/NodeJs/nedb) 라이브러리
- Oracle DB (사용법 세팅중)

## 개발 환경 구성

Node.js가 설치되어있다는 가정하에 시작.
Database는 nedb 사용시 가이드에 맞춰 진행. 
기타 DB사용할 경우 상단의 Database 문서 참고하여 설치후 가이드 따라서 진행.

### 개발 폴더 구성

BackEnd 및 FrontEnd가 구성될 폴더를 지정합니다.
예제에서는 `C:\study` 폴더가 메인입니다.
우선 `C:\study` 빈 폴더를 만들면 개발 폴더 구성은 완료입니다!

### Template Project 생성

BackEnd 서버 및 FrontEnd 서버를 구성 및 연동하는 방법입니다.

#### Express API BackEnd 서버 생성

`C:\study` 경로에서 CMD 창을열어 다음 명령어를 입력합니다.

```Batch
npm install -g express-generator
```

위 명령어는 Express Application을 쉽게 생성해주는 Express Generator를 설치하며, 한번 설치했으면 다음 프로젝트를 생성할때마다 실행할 필요가 없습니다.

그다음 다음 명령을 입력하여 `be`라는 이름의 BackEnd Application을 생성합니다.

```Batch
express be
cd be
npm install
cd ..
```

명령어 실행 이후 `C:\study\be` 폴더가 정상적으로 생겼다면 Application 생성이 완료된것입니다.

이제 Port를 지정하겠습니다. be폴더안의 package.json을 열어 start 부분을 다음과 같이 수정합니다.

```js
{
  ... 생략
  "scripts": {
    "start": "set PORT=3001 && node ./bin/www"
  },
  ... 생략
}
```

이렇게 세팅할 경우 BackEnd 서버가 `3001`번 포트로 실행됩니다. 만약 다른 포트를 지정하고 싶으시면 바꾸셔도 됩니다.

`be` 폴더에서 다음 명령을 실행할 경우 서버가 실행되지만, 코드를 바꿀때마다 서버를 닫고 다시 열어야 하는 번거로움이 있습니다.

```Batch
npm start
```

BackEnd 코드가 변경됨에 따라 자동으로 서버를 재시작 하는 nodemon 라이브러리 설치를 위해 다음 명령을 입력합니다.

```Batch
npm install nodemon
```

그다음 `be`폴더의 `package.json`을 다음과 같이 수정합니다.

```js
{
  ... 생략
  "scripts": {
    "start": "set PORT=3001 && nodemon ./bin/www"
  },
  ... 생략
}
```

그다음 다시 다음 명령을 실행하여 정상적으로 `nodemon` 으로 올라오는지 확인합니다.

```batch
npm start
```

정상적으로 실행이 될 경우 다음과 같이 나올것입니다.

![nodemon_success.png](/study/noticeboard/nodemon_success.png)

이제 기초적인 BackEnd 서버는 세팅이 끝났습니다. 다음 스탭을 통해 React로 FrontEnd 서버를 구성하는 방법을 참고하세요.

#### React FrontEnd 서버 생성

다시 최상단 폴더인 `c:\study` 로 이동하여 진행합니다.

다음 명령을 입력하여 React Application을 생성하는 라이브러리를 설치합니다. Express-Generator와 마찬가지로 한번 설치 이후에 다시 재설치 할 필요가 없습니다.

```Batch
npm install -g create-react-app
```

성공했으면 다음 명령을 통해 `fe`라는 이름을 가진 FrontEnd 프로젝트를 생성합니다.

```Batch
create-react-app fe
```

`c:\study\fe`폴더가 정상적으로 생성되었으면 프로젝트가 잘 만들어 진겁니다.

`c:\study\fe` fe폴더 안의 `package.json`을 열어 다음과 같이 수정합니다.

```js
{
  ... 생략
  "scripts": {
   "start": "react-scripts start",
   "build": "react-scripts build",
   "test": "react-scripts test --env=jsdom",
   "eject": "react-scripts eject"
  },
  "proxy": "http://localhost:3001"
}
```

여기서 `http://localhost:3001`는 위에서 설정한 BackEnd의 EndPoint입니다.

이제 다음 명령을 입력하여 FrontEnd 서버를 실행합니다. (기본 포트는 3000입니다.)

```batch
npm start
```

정상적으로 실행되면 http://localhost:3000 으로 접속하여 다음 화면이 나오는지 확인합니다.

<img src="/study/noticeboard/react_complete.png" width="450" style="max-width: 100%;">

화면이 나왔으면 FrontEnd 환경구성도 완료됬습니다. 이제 다음 스탭을 통해 BackEnd서버와 FrontEnd서버간의 데이터를 연결하겠습니다.

#### BackEnd <-> FrontEnd 통신 설정

눈치가 빠르신 분들은 이해하셨겠지만 FrontEnd의 `package.json`의 proxy 설정이 BE <-> FE간 통신의 베이스 입니다.

FrontEnd에서 보내는 통신을 BackEnd에 보내서 처리해주기 때문에 복잡한 구성없이 연동이 가능합니다.

`C:\study\be\routes` 폴더의 index.js를 열어 다음과 같이 수정합니다.

`C:\study\be\routes\index.js 전체 코드`
```js
var express = require('express');
var router = express.Router();

/* GET home page. */
router.get('/api/main', function(req, res, next) {
  res.send({
    response: "BackEnd Response Data"
  });
});

module.exports = router;
```

이렇게 설정한뒤 http://localhost:3001/api/main 으로 접속 할 경우 다음과 같이 출력될 것입니다.

```json
{response: "BackEnd Response Data"}
```

이걸 FrontEnd 에서 통신하여 Main화면에 띄워보겠습니다.

`C:\study\fe\src` 폴더의 `App.js` 파일을 열어 다음과 같이 수정하겠습니다. 
이번에도 전체 소스코드입니다. 어디가 바뀌는지 하나씩 보셔도 되고, 전체 Copy하셔도 됩니다.

```js
import React, {useState, useEffect} from 'react';
import logo from './logo.svg';
import './App.css';

function App() {
	const [data,setData] = useState("");
	useEffect(() => {
		async function loadData(){
			let response = await (await fetch("/api/main")).json();
			setData(response.response);
		}
		
		loadData();
	});
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
			{data}
        </p>
      </header>
    </div>
  );
}

export default App;
```

그러면 다음과 같이 위에서 입력한 `BackEnd Response Data` 가 출력됩니다.

제대로 연동됬는지 확인을 위해 BackEnd의 값을 바꿔가면서 새로고침 해보세요. 

잘 바뀐다면 이제 DB 연동을 할 차례입니다.

### Tabset {.tabset}
#### Node.js nedb 사용

#### Oracle SQL 사용 (작성중)

#### PostgreSQL 사용 (작성중)


## 참여자
<table>
  <tr>
    <td>
      <a href="https://github.com/zeliper">
        <img src="https://github.com/zeliper.png?size=250" width="115" style="max-width: 100%;">
        <br/>
        <center>오승우<br/>(Zeliper)</center>
      </a>
    </td>
    <td style="align-contents: center">
      <a href="https://github.com/SANAI-HWANG">
        <img src="https://github.com/SANAI-HWANG.png?size=250" width="115" style="max-width: 100%;">
        <br/>
        <center>황순상<br/>(SANAI-HWANG)</center>
      </a>
    </td>
    <td>
      <a href="https://github.com/JanGeeSangHyeok">
        <img src="https://github.com/JanGeeSangHyeok.png?size=250" width="115" style="max-width: 100%;">
        <br/>
        <center>박상혁<br/>(JanGeeSangHyeok)</center>
      </a>
    </td>
  </tr>
</table>