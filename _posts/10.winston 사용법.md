`winston`은 Node.js에서 가장 인기 있는 로깅 라이브러리 중 하나로, 로그의 생성, 전송, 쿼리 등을 다루기 위한 다양한 기능을 제공합니다. `winston`을 사용하면 로그 레벨 설정, 다양한 저장소(트랜스포트)로의 로그 출력, 커스텀 포맷팅 등을 쉽게 구성할 수 있습니다.

### Winston 설치

`winston`을 사용하기 전에, 먼저 npm을 사용하여 패키지를 프로젝트에 설치해야 합니다.

```bash
npm install winston
```

### 기본 사용법

`winston`에서 로거 인스턴스를 생성하고, 이를 사용하여 로그를 기록하는 기본적인 방법은 다음과 같습니다.

```javascript
const winston = require('winston');

const logger = winston.createLogger({
  level: 'info', // 최소 로그 레벨 설정
  format: winston.format.json(), // 로그 포맷 설정
  transports: [
    //
    // - 콘솔로 로그 출력
    new winston.transports.Console(),
    //
    // - 파일로 로그 저장
    new winston.transports.File({ filename: 'error.log', level: 'error' }),
    new winston.transports.File({ filename: 'combined.log' })
  ]
});

// 로그 기록
logger.info('Hello, this is a logging message.');
logger.error('This is an error message');
```

### 로그 레벨

`winston`은 다양한 로그 레벨을 지원합니다. 기본적으로 `{ error: 0, warn: 1, info: 2, http: 3, verbose: 4, debug: 5, silly: 6 }` 레벨을 사용하며, 설정한 레벨 이상의 중요도를 가진 로그만이 기록됩니다.

### 커스텀 포맷

`winston`의 `format` 모듈을 사용하면 로그 메시지의 포맷을 커스텀할 수 있습니다. 예를 들어, 타임스탬프를 추가하거나 로그 메시지 형식을 변경할 수 있습니다.

```javascript
const logger = winston.createLogger({
  format: winston.format.combine(
    winston.format.timestamp({
      format: 'YYYY-MM-DD HH:mm:ss'
    }),
    winston.format.printf(info => `${info.timestamp} ${info.level}: ${info.message}`)
  ),
  transports: [new winston.transports.Console()]
});
```

### 다양한 트랜스포트 사용

`winston`은 로그를 여러 대상에 기록할 수 있는 트랜스포트 시스템을 제공합니다. 예를 들어, 파일, 콘솔, HTTP 서비스 등 다양한 출력 대상으로 로그를 보낼 수 있습니다.

```javascript
const logger = winston.createLogger({
  transports: [
    new winston.transports.Console(),
    new winston.transports.File({ filename: 'combined.log' }),
    // 추가적인 트랜스포트 구성 가능
  ]
});
```

`winston` 로거의 주요 옵션들을 아래 표에 정리해 보았습니다. 이 옵션들은 로거를 생성할 때 `createLogger` 함수에 전달되는 설정 객체에서 사용됩니다.

| 옵션          | 설명                                                         | 예시                                    |
|---------------|------------------------------------------------------------|---------------------------------------|
| `level`       | 로거에 설정할 최소 로그 레벨. 이 레벨 이상의 로그만 기록됩니다.   | `'info'`, `'error'`                   |
| `format`      | 로그 메시지의 포맷을 결정하는 `winston.format`의 인스턴스입니다. | `winston.format.json()`, `winston.format.simple()` |
| `transports`  | 로그 메시지를 출력할 대상을 정의합니다. 배열 형태로 여러 개를 지정할 수 있습니다. | `[new winston.transports.Console()]`, `[new winston.transports.File({ filename: 'combined.log' })]` |
| `defaultMeta` | 모든 로그 메시지에 기본적으로 포함될 메타데이터 객체입니다.    | `{ service: 'user-service' }`        |

`transports` 옵션에서 사용할 수 있는 `winston`의 기본 트랜스포트 옵션들을 추가로 정리해 보았습니다.

| 트랜스포트           | 설명                                                         | 주요 옵션                                                     |
|---------------------|------------------------------------------------------------|-------------------------------------------------------------|
| `Console`           | 콘솔로 로그를 출력합니다.                                     | `level`, `format`                                            |
| `File`              | 로그를 파일로 기록합니다.                                     | `filename`: 로그 파일 경로, `level`, `format`, `maxsize`: 파일 최대 크기, `maxFiles`: 보관할 최대 파일 수 |
| `Http`              | 로그를 HTTP로 전송합니다.                                      | `level`, `format`, `url`: 로그를 전송할 URL                  |

`winston`은 커스텀 트랜스포트를 생성하는 기능도 제공하므로, 사용자 정의 로깅 요구사항에 맞게 확장할 수 있습니다. 이는 `winston.Transport`를 상속받아 구현할 수 있습니다.


`winston`을 사용하면, 애플리케이션 로깅 요구사항에 맞게 매우 유연한 로깅 시스템을 구축할 수 있습니다. 다양한 설정과 옵션을 조합하여 필요한 로깅 솔루션을 만들 수 있습니다.