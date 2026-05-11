# 포트폴리오 슬라이드

---

## Slide 01 | 표지 / 자기소개

이름: 박중현
포지션: Backend Engineer
소속: Dktechin a kakaocompany (현재)
경력: 6년차 (2020 ~)

> 고객 상담 시스템(CS)의 백엔드 개발과 통계 데이터 정합성 운영을 담당하며,
> 운영 리스크를 최소화하는 서비스 구조 설계를 주도해 왔습니다.

연락처: kos5667@gmail.com
GitHub: https://github.com/kos5667

---

## Slide 02 | 커리어 여정

[ 이미지: 좌우 타임라인 - 재하정보기술(2020~2022) / Dktechin(2022~현재) 구간 표시, Dktechin 내 3개 페이즈 분기 ]

핵심 도메인 변화

- 공간정보 / 공공 행정 (재하정보기술)
- 대규모 CS 플랫폼 / 실시간 메시징 / 통계 (Dktechin)

공통 역량

- Java, Spring Boot 기반 백엔드 개발
- RDBMS 설계 및 쿼리 최적화
- 서비스 운영 중 이슈 개선

---

## Slide 03 | 카카오 CS 플랫폼 개요 - 대규모 실시간 상담 시스템

[ 이미지: 전체 시스템 구성도 - 수신 서버(Spring Boot) / 상담 서버(Node.js) / Kubernetes / RabbitMQ / Redis / DB 관계 ]

서비스 소개

카카오 전사 고객 상담을 처리하는 실시간 상담톡 플랫폼 전담 운영.
고가용성과 무중단 운영이 핵심 요구사항인 환경에서 안정성과 확장성을 지속 개선했습니다.

담당 범위

- Spring Boot 3.4 / Java 21 기반 수신 서버 설계 및 운영
- RabbitMQ 기반 수신 서버-상담 서버 간 메시지 전달 구조 운영
- Kubernetes 인프라 전반 (배포 구조, CI/CD, HPA)
- Node.js 기반 실시간 상담 서버 운영 (실시간 메시징, 상담 배분, 통계)
- Multi IDC 고가용성 구조 설계

기술 스택

Spring Boot 3.4 / Java 21, MySQL, Redis, RabbitMQ, Kubernetes, Bucket4j, Vault,
Node.js / TypeScript / Express / Socket.io, Vue3

기간: 2022.07 ~ 현재 | 단독 운영 | 기여도 100%

---

## Slide 04 | Multi IDC 고가용성 아키텍처 설계

[ 이미지: Before / After 구조도 - Before: GSLB → IDC-A 집중 / After: GSLB → 3개 IDC → Kubernetes Client Service → Backend 균등 분배 ]

배경

Multi IDC 도입 후 IDC-A에 트래픽 80% 이상이 집중되는 문제 발생.
운영 안정성과 장애 대응력이 저하될 수 있는 상황.

원인 분석

GSLB 분배 정책에는 두 가지 방식이 있음.

- A (균등 분배): 트래픽을 모든 리전에 동일 비율로 분산 → 정상 동작
- B (가중 분배): 한 리전에 집중적으로 트래픽을 보낸 뒤 일정 구간 후 다른 리전으로 전환

B 정책 적용 구간에서 IDC-A로 트래픽이 집중되고, DNS 캐싱으로 인해
정책 전환 후에도 클라이언트가 IDC-A로 계속 라우팅되는 현상 지속.

GSLB A정책으로 전환하면 해소되지만, 운영에서 검증되지 않은 정책 변경은 리스크가 컸습니다.
클러스터 내부에서 처리 가능하다고 판단해 Kubernetes 레벨에서 트래픽을 재분산하는 방향을 선택했습니다.

해결 방식

DNS 캐싱 우회를 위해 GSLB 레벨이 아닌 Kubernetes 클러스터 내부에서 트래픽을 재분산.

- Ingress에 경로 기반 라우팅 추가: `/`는 Client Service(FE), `/api` `/tools`는 Server Service(BE)로 분리
- Service 객체는 라우팅 규칙을 정의해 etcd에 저장하고, Control Plane이 이를 각 Node에 전파
- 실제 트래픽 전달은 각 Node의 Cilium이 담당: Service 규칙에 따라 적절한 Pod IP로 전달
- Cilium VXLAN 터널링으로 Node 간 Pod 라우팅을 투명하게 처리

결과

- Multi IDC 환경 무중단 운영 구조 확보
- 트래픽 급증 시에도 수평 확장 가능한 기반 마련
- 장애 발생 시 IDC 단위 격리 및 대응 체계 확보

---

## Slide 05 | 분산 환경 안정성 확보 - Rate Limiting & 분산락

[ 이미지: 두 문제를 나란히 - 왼쪽: 다중 Pod Rate Limiting 흐름(Redis 공유 상태), 오른쪽: 분산락으로 후처리 단일 실행 제어 흐름 ]

문제 1. 어뷰징 감지 - 다중 Pod 환경에서 사용자별 요청 제어

- Kubernetes Pod 간 상태를 공유하지 않아 개별 Pod 단위 Rate Limit으로는 어뷰징 감지 불가
- Redis + Bucket4j Token Bucket 알고리즘으로 분산 상태 공유 기반 Rate Limiting 구현
- 차단 대신 알람 정책 채택으로 정상 사용자 오차단 0건

문제 2. 후처리 중복 실행 - 다중 Pod 동시 실행 제어

- 상담 종료 이벤트를 여러 Pod가 동시에 수신해 후처리 로직이 중복 실행되는 문제
- Redis 분산락 (SET NX PX) 으로 동일 채팅방 후처리 동시 실행 제어
- 멱등성 보장으로 운영 이슈 제거

문제 3. 카테고리 트리 탐색 - DFS 재귀 구조의 스택 오버플로우 리스크

- 카테고리 뎁스 증가에 따라 DFS 재귀 탐색의 스택 오버플로우 위험과 성능 저하가 누적되는 문제
- DFS 재귀 탐색을 BFS로 전환해 뎁스와 무관한 안정적 탐색 구조 확보
- 초기화 시간은 동일하게 유지하면서 뎁스 탐색 시간 ms 단위 단축

공통 설계 원칙

정상 사용자에게 영향을 주지 않으면서 비정상 케이스만 격리.

---

## Slide 06 | 배포 구조 개선 - 단위 분리와 무중단 운영

[ 이미지: Before / After Pod 구조 - Before: FE+BE 하나의 Pod / After: FE Pod, BE Pod 분리, 빌드 시간 비교 ]

배경

단일 Region으로 운영하던 시절 데이터센터 화재로 장시간 운영 장애 발생.
운영 리스크를 줄이고자 Multi IDC를 도입했고, 이에 맞춰 Container 분리 작업을 병행해
리소스 배분 최적화와 장애 대응 속도 향상을 함께 도모했습니다.

Before

- FE / BE / Batch가 하나의 Multi-Container Pod로 묶여 있어 하나만 변경해도 전체 재빌드
- FE 변경 하나에도 BE 이미지를 함께 빌드하고 Pod 전체를 교체
- 배포 단위가 크고 롤백 범위가 넓어 핫픽스 대응 속도 저하

After

- FE / BE / Batch를 Single-Container Pod로 분리해 독립 배포 구조로 전환
- 카나리 / 블루그린 배포 전략 적용 가능한 구조 확보

수치 비교

|  | Build | Deploy | Resource |
|---|---|---|---|
| Before | FE 5~8분, BE 5~8분 | FE 3~5분, BE 3~5분 | FE 8개, BE 8개 |
| After | FE 1분, BE 2~3분 | FE 1분, BE 2~3분 | FE 2개, BE 8개 유지 |

효과

- 핫픽스 및 장애 대응 리드타임 감소
- FE 리소스 8개 → 2개로 축소, 불필요한 자원 낭비 제거
- 서비스별 독립 모니터링 및 스케일링 가능

---

## Slide 07 | 보안 강화 - Vault & AES-GCM 암호화 체계

[ 이미지: Vault 시크릿 관리 흐름 - 코드 → Vault 런타임 주입 → 서비스 간 AES-GCM 암호화 통신 ]

수행 내용

- Vault 기반 키 관리 체계 도입: 서비스별 시크릿 중앙 관리, 런타임 주입
- AES-GCM 암호화 적용: 서버 간 인증 및 민감정보 보호 모듈 구현
- 소스 내 Secret(계정정보, 암호화 키) 평문 노출 제거
- Spring Security 6 기반 세션 보안 설정 강화
- ISMS-P 인증 대응: 보안 점검 및 취약점 개선

설계 원칙

- 시크릿은 코드에 포함하지 않고 Vault에서 런타임에 주입
- 서비스 간 통신에 암호화 기반 인증 적용

결과

- 민감정보 노출 리스크 제거
- 보안 감사 및 인증 대응 기반 확보

---

## Slide 08 | 통계 데이터 정합성 - 운영 판단 오류 리스크 제거

[ 이미지: 배치 파이프라인 흐름도 - 집계 배치 실행 → 수치 불일치 감지 → SQL/서비스 레이어 추적 → 보정 로직 적용 ]

배경

카카오 고객센터 운영자가 매일 사용하는 통계 조회 / 배치 / Excel 출력 서비스.
수치 불일치 이슈가 반복되며 운영자 의사결정의 신뢰성 저하.

문제

- 그룹별 실적 / 상담원 현황 / 주간 집계 수치가 맞지 않는 케이스 반복 발생
- 특정 일자 누락 데이터, 장기 미처리 문의 집계 오류

접근 방식

- 조회 SQL과 배치 SQL 결과를 항목별로 대조해 수치가 갈라지는 구간 특정
- 특정 일자 범위에서 집계 배치가 스킵되는 패턴 확인, 누락 데이터 복구 로직 추가
- 배치 파이프라인에 보정 처리 단계를 삽입해 재발 방지

결과

- 수치 불일치 반복 이슈 제거
- 신뢰 불가 데이터로 인한 운영 판단 오류 리스크 제거
- 운영 데이터 신뢰도 확보

---

## Slide 09 | CRMS 서비스 현대화 - 마이그레이션 / 구조 분리

[ 이미지: 전환 항목 체크리스트 - 레거시 VM → Kubernetes, 단일 서버 → API 분리 ]

배경

CRMS 통계 서비스가 EOL 임박한 레거시 환경에서 운영 중.
API 기능 혼재로 변경 영향 범위도 계속 확대되는 상황.

프레임워크 마이그레이션 (단독 수행)

- javax → jakarta 네임스페이스 전환 (전 레이어)
- Spring Security 6 대응: WebSecurityConfigurerAdapter 제거, 람다 기반 DSL로 재작성
- RestTemplate → WebClient 전환 및 외부 연동 재정비
- VM 기반 → Kubernetes(DKOS) 배포 전환: Dockerfile / Vault 설정 / Kustomize 오버레이 정비
- ShedLock 기반 분산 배치 락 적용

API 서버 분리 (2023.11 ~ 2024.07 | 구성: 4명 | 기여도 40%)

- RESTful 기반 CRMS-API 전담 서버를 신규 설계 및 점진 이관
- Springdoc OpenAPI 기반 API 문서화 및 표준 응답 규격 / 공통 Exception Handler 정비
- ACL 강화, CORS 정책 재정의

결과

- EOL 프레임워크 위험 해소 및 보안 취약점 대응 기반 마련
- API 서버 독립 배포로 변경 영향 범위 축소, CRMS 본 시스템 부하 분산

---

## Slide 10 | 아키텍처 현대화 - 운영 중단 없는 레거시 개선 전략

[ 이미지: Strangler Fig 패턴 단계별 진행 - 기존 구조에서 도메인 단위로 점진 교체되는 흐름 ]

배경

단일 파일 3,000줄 이상, 메서드 50개 이상으로 비대해진 구조에서
기능 하나를 수정할 때 영향 범위 파악이 어렵고 온보딩 비용도 높은 상황.
운영 중인 서비스를 중단 없이 개선해야 하는 제약.

Before - 기술 중심 패키지 구조

```
src/
├── controllers/    ← 비즈니스 로직이 컨트롤러에 혼재
├── models/         ← I/O 모델, 도메인, 캐시가 같은 파일에 공존
├── services/       ← 도메인 로직 없이 유스케이스 처리 집합소
└── routes/
```

After - 도메인 중심 구조

```
src/
├── domains/
│   └── agent/
│       ├── AgentEntity        ← 도메인 엔티티
│       ├── AgentRepository    ← 도메인 저장소 인터페이스 (추상화)
│       └── AgentEvents        ← 도메인 이벤트 정의
├── application/
│   └── agent/
│       └── AgentApplicationService  ← 유스케이스 처리(트랜잭션 단위)
├── infrastructure/
│   └── repository/
│       ├── persistence/       ← ORM 기반 저장소 구현
│       └── caching/           ← Redis 기반 캐시 구현
├── interfaces/                ← 입출력 인터페이스 모음
│   └── AgentController        ← HTTP 핸들러
└── routes/
    ├── HttpRouter             ← RESTful HTTP 요청 라우팅
    ├── GrpcRouter             ← gRPC 프로토콜 라우팅
    └── SocketRouter           ← 실시간 Socket 이벤트 라우팅
```

전략: Strangler Fig 점진 이관

- 변경 영향이 큰 영역부터 순차적으로 리팩토링, 운영 리스크 통제
- 도메인 경계를 명확히 하고 인터페이스 기반으로 의존성 역전(DIP) 적용
- 테스트 커버리지를 핵심 플로우 중심으로 먼저 확보한 뒤 리팩토링 범위 확장

결과

- 구조 정리로 변경 영향 범위 축소, 유지보수성 개선
- 회귀 리스크 감소로 배포 안정성 향상
- 온보딩 비용 절감

---

## Slide 11 | K-GeoPlatform - ETL 파이프라인 & 대용량 데이터 처리

[ 이미지: ETL 파이프라인 흐름도 - 데이터 수집(크롤링/변동) → Spring Batch 처리 → DW 적재 → 시각화 ]

프로젝트 개요

국토교통부 K-GeoPlatform 1, 2차 구축 사업 참여.
공간정보 데이터 통합 관리 및 부동산/행정 도메인 서비스 개발.

기간: 2020.06 ~ 2022.04 | 재하정보기술

주요 문제 해결

- 대용량 Join 병목: 17개 시도 코드별 테이블 반복 Join을 파티션 구조 개선으로 해소
- ETL 자동화: Spring Batch + Quartz 기반 데이터 변동 처리 파이프라인 설계/구축
- 공간 데이터 처리: PostGIS 공간 쿼리 기반 좌표 추출 및 위치 정확도 향상
- 다중 RDBMS 운영: Oracle / PostgreSQL / Tibero Migration 및 DW/DM 구축

기술 스택

Java, Spring Boot, Spring Batch, Quartz, MyBatis, PostgreSQL, PostGIS, Oracle, Tibero

---

## Slide 12 | 기술 스택 & 핵심 역량

[ 이미지: 기술 스택 시각화 - 분류별 아이콘 또는 그리드 레이아웃 ]

Backend

Java 21, Node.js (TypeScript)
Spring Boot, Spring MVC, Spring Security 6, Spring Batch, Spring Data JPA, Spring Data Redis
Express, Socket.io, Vue3
JPA, QueryDSL, MyBatis
JUnit 5, Mockito, Jest
Gradle, Maven

Database & Messaging

MySQL, PostgreSQL (PostGIS), Oracle, Tibero
Redis (캐시, 세션, 분산락)
RabbitMQ (AMQP)

DevOps & Infra

Kubernetes (Ingress, HPA, Kustomize), Docker
Jenkins
Vault, AES-GCM, JWT, ACL, ISMS-P
Bucket4j, ShedLock
배포 전략: Rolling, Canary, Blue-Green
Multi IDC / Multi Region
Linux (CentOS)
Git, Jira, Confluence

---

## Slide 13 | 지향점

개선 과제를 스스로 찾습니다

이슈가 들어오기를 기다리기보다, 서비스와 코드를 직접 관찰하며
잠재적인 리스크와 개선 포인트를 먼저 파악합니다.
방향을 고민하고 설계해 실행으로 이어지는 방식으로 일합니다.

구현보다 원인을 먼저 봅니다

복잡한 구현이 필요한 문제보다, 현상의 원인을 명확히 파악하고
현재 상황에서 최적의 개선 방향을 설계하는 것을 우선합니다.

운영 리스크를 먼저 생각합니다

기능을 빠르게 만드는 것보다, 장애가 났을 때 얼마나 빠르게 원인을 파악하고
영향 범위를 줄일 수 있는지를 먼저 고려합니다.

운영과 개발을 함께 봅니다

실서비스 운영 경험을 바탕으로 모니터링, 장애 대응, 배포 전략까지
개발과 운영을 하나의 흐름으로 다룹니다.

구조가 설명을 대신합니다

도메인 경계가 명확하고 의존성이 정리된 코드는 문서 없이도 읽힙니다.
설계 판단과 그 근거를 남기는 습관을 유지합니다(물론 주석과 문서도 작성합니다!).

---
