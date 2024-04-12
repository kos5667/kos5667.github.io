---
layout: post
title:  "Node.js, Express를 이용한 Project"
subtitle: javascript, Node.js 그리고 Express를 이용한 Project 생성 방법
date:   2024-02-28 09:00:00 +0900
excerpt_image: "../assets/images/excerpt-node-js-project.png"
banner:
  image: "../assets/images/banners/banner-node-js-project.png"
  loop: true
  volume: 0.8
  opacity: 0.618
  background: "#000"
  height: "100vh"
  min_height: "38vh"
  heading_style: "font-size: 4.25em; font-weight: bold; text-decoration: underline"
  subheading_style: "color: gold"
categories: Node.js
tags: [node.js, express, javascript, npm, project]
---

## Node.js & Express
**Node.js**는 Chrome V8 자바스크립트 엔진으로 빌드된 크로스 플랫폼 런타임 환경입니다. 
이를 통해 개발자들은 서버 사이드 및 네트워킹 애플리케이션을 자바스크립트로 쉽게 구축할 수 있습니다. 
Node.js는 이벤트 기반, 비동기식 프로그래밍을 지원하며 이는 입출력 처리에서 높은 성능을 발휘합니다. 
주로 웹 서버를 구축할 때 많이 사용됩니다.

**Express**는 Node.js를 위한 가장 인기 있는 웹 프레임워크 중 하나입니다. 
이 프레임워크는 웹 및 모바일 애플리케이션 개발을 위한 강력한 기능 세트를 제공합니다. 
Express는 미들웨어 아키텍처를 사용하여 서버 사이드 로직을 구성하는 데 유용합니다. 
사용자 요청에 대한 응답을 처리하거나 데이터베이스 쿼리를 실행하는 등의 작업을 간편하게 할 수 있도록 도와줍니다.

간단하게 말해서, Node.js는 자바스크립트를 이용하여 서버의 백엔드 로직을 실행할 수 있는 환경을 제공하고, Express는 이 환경 위에서 웹 애플리케이션을 보다 쉽게 개발할 수 있도록 도와주는 프레임워크입니다. 
Express를 사용함으로써 라우팅, 세션 관리, 사용자 인증 등의 기능을 쉽게 구현할 수 있습니다.

### 1. Node.js 설치
프로젝트를 시작하기 전에, Node.js가 설치되어 있어야 합니다. Node.js는 [공식 웹사이트](https://nodejs.org/)에서 다운로드할 수 있습니다. 
설치를 마쳤다면, 터미널에서 다음 명령어를 입력하여 Node.js와 npm(npm은 Node.js 패키지 관리자입니다)이 정상적으로 설치되었는지 확인합니다.

```bash
node -v
npm -v
```

### 2. 프로젝트 디렉토리 생성 및 초기화

프로젝트에 사용할 새 디렉토리를 만들고, 그 디렉토리로 이동합니다.

```bash
mkdir my-node-project
cd my-node-project
```

npm을 사용하여 새 Node.js 프로젝트를 초기화합니다. 이 명령어는 `package.json` 파일을 생성하는데, 이 파일은 프로젝트의 메타데이터와 의존성을 관리합니다.

```bash
npm init -y
```

### 3. Express 설치

npm을 통해 Express를 프로젝트에 설치합니다.

```bash
npm install express
```

### 4. 애플리케이션 파일 생성

프로젝트의 루트 디렉토리에 `app.js` 파일을 생성합니다. 이 파일은 Express 애플리케이션의 진입점이 됩니다.

```javascript
const express = require('express');
const app = express();
const port = 3000;

app.get('/', (req, res) => {
  res.send('Hello World!');
});

app.listen(port, () => {
  console.log(`Example app listening at http://localhost:${port}`);
});
```

### 5. 애플리케이션 실행

위 코드를 `app.js` 파일에 저장한 후, 터미널에서 다음 명령어를 실행하여 애플리케이션을 시작합니다.

```bash
node app.js
```

브라우저를 열고 `http://localhost:3000`으로 접속하면, "Hello World!" 메시지를 볼 수 있습니다.

### 6. 개발 의존성 추가 (선택사항)

개발 중에는 코드 변경을 자동으로 감지하고 서버를 재시작해주는 `nodemon` 같은 도구를 사용하는 것이 편리합니다.

```bash
npm install --save-dev nodemon
```

`package.json` 파일에서 `scripts` 부분을 수정하여 `nodemon`을 사용하도록 설정할 수 있습니다.

```json
"scripts": {
  "start": "node app.js",
  "dev": "nodemon app.js"
}
```

이제 `npm run dev` 명령어로 개발 서버를 시작할 수 있습니다.

이 가이드를 통해 기본적인 Express 애플리케이션을 설정하고 실행하는 방법을 알아보았습니다. Express는 매우 유연한 프레임워크이므로, 추가적인 기능이나 미들웨어를 통해 애플리케이션을 확장할 수 있습니다.