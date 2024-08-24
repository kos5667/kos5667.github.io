`body-parser`는 Express.js 애플리케이션에서 HTTP 요청 본문을 파싱하는 데 사용되는 미들웨어입니다. 클라이언트로부터 오는 요청의 본문(body)을 쉽게 추출할 수 있게 해주어, 서버에서 이 데이터를 사용하여 다양한 작업을 수행할 수 있습니다.

`body-parser` 미들웨어는 주로 JSON 데이터나 URL 인코딩된 데이터를 처리하는 데 사용됩니다. Express.js 4.16.0 버전 이후부터는 `body-parser`의 기능이 Express에 내장되어 별도로 설치할 필요 없이 사용할 수 있게 되었습니다.

### body-parser 사용 예시

Express.js에서 `body-parser`를 사용하는 예전 방식은 다음과 같습니다:

```javascript
const bodyParser = require('body-parser');
const express = require('express');
const app = express();

// JSON 형식의 본문을 파싱하기 위해
app.use(bodyParser.json());

// URL 인코딩된 데이터를 파싱하기 위해
app.use(bodyParser.urlencoded({ extended: true }));
```

Express 4.16.0 이상에서는 `express` 모듈 자체에서 이 기능을 제공하므로 다음과 같이 사용할 수 있습니다:

```javascript
const express = require('express');
const app = express();

// JSON 형식의 본문을 파싱하기 위해
app.use(express.json());

// URL 인코딩된 데이터를 파싱하기 위해
app.use(express.urlencoded({ extended: true }));
```

### 주요 기능

- **JSON 데이터 파싱**: 클라이언트로부터 받은 JSON 형식의 데이터를 JavaScript 객체로 변환합니다.
- **URL 인코딩된 데이터 파싱**: 클라이언트가 `application/x-www-form-urlencoded` 미디어 타입으로 보낸 요청 본문을 파싱합니다. 이는 HTML 폼 데이터의 처리에 주로 사용됩니다.
- **원시 데이터(raw data) 및 텍스트 데이터(text data) 파싱**: 드물게 사용되지만, `body-parser`는 텍스트 형식의 본문이나 원시 데이터의 본문 처리도 지원합니다.

### 사용법

Express 내장 파서를 사용하여 애플리케이션에서 HTTP 요청 본문을 쉽게 처리할 수 있습니다. 이를 통해 API 개발 시 클라이언트로부터 전송받은 데이터를 효율적으로 사용하고 관리할 수 있습니다.