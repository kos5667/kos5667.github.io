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
- RabbitMQ 메시징 파이프라인 관리
- Kubernetes 인프라 전반 (배포 구조, CI/CD, HPA)
- Node.js 기반 실시간 상담 서버 운영 (실시간 메시징, 상담 배분, 통계)
- Multi IDC 고가용성 구조 설계

기술 스택

Spring Boot 3.4 / Java 21, MySQL, Redis, RabbitMQ, Kubernetes, Bucket4j, Vault,
Node.js / TypeScript / Express / Socket.io, Vue3

기간: 2022.07 ~ 현재 | 단독 운영 | 기여도 100%

---

## Slide 04 | Multi IDC 고가용성 아키텍처 설계

[ 이미지: Before / After 구조도 - Before: IDC-A에 트래픽 집중 / After: IPVS 기반 2차 분산으로 IDC-A, IDC-B 균등 분배 ]

배경

Multi IDC 도입 후 IDC-A에 트래픽 80% 이상이 집중되는 문제 발생.
운영 안정성과 장애 대응력이 저하될 수 있는 상황.

원인 분석

- DNS 캐싱으로 인해 클라이언트가 동일 IDC로 지속 라우팅
- Ingress 레벨에서 트래픽 제어가 불가한 구조

해결 방식

- Kubernetes 내부 Client Service 추가
- IPVS 기반 2차 트래픽 분산으로 IDC 간 부하 균등화

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

공통 설계 원칙

정상 사용자에게 영향을 주지 않으면서 비정상 케이스만 격리.

---

## Slide 06 | 배포 구조 개선 - 단위 분리와 무중단 운영

[ 이미지: Before / After Pod 구조 - Before: FE+BE 하나의 Pod / After: FE Pod, BE Pod 분리, 빌드 시간 비교 ]

Before

- FE / BE가 하나의 Multi-Container Pod로 묶여 있어 둘 중 하나 변경 시 전체 재빌드
- 빌드 시간: 5 ~ 8분
- 배포 단위가 크고 롤백 범위가 넓어 핫픽스 대응 속도 저하

After

- FE / BE를 Single-Container Pod로 분리해 독립 배포 구조로 전환
- 빌드 시간: FE / BE 각 1분 이내
- 카나리 / 블루그린 배포 전략 적용 가능한 구조 확보

효과

- 핫픽스 및 장애 대응 리드타임 감소
- 변경 영향 범위 축소로 배포 안정성 향상
- 서비스별 독립 스케일링 가능

---

## Slide 07 | 통계 데이터 정합성 - 운영 판단 오류 리스크 제거

[ 이미지: 배치 파이프라인 흐름도 - 집계 배치 실행 → 수치 불일치 감지 → SQL/서비스 레이어 추적 → 보정 로직 적용 ]

배경

카카오 고객센터 운영자가 매일 사용하는 통계 조회 / 배치 / Excel 출력 서비스.
수치 불일치 이슈가 반복되며 운영자 의사결정의 신뢰성 저하.

문제

- 그룹별 실적 / 상담원 현황 / 주간 집계 수치가 맞지 않는 케이스 반복 발생
- 특정 일자 누락 데이터, 장기 미처리 문의 집계 오류

접근 방식

- MyBatis SQL과 서비스 레이어를 병행 추적해 원인 구간 특정
- 누락 데이터 복구 로직 추가, 배치 파이프라인 보정 처리 구현

결과

- 수치 불일치 반복 이슈 제거
- 신뢰 불가 데이터로 인한 운영 판단 오류 리스크 제거
- 운영 데이터 신뢰도 확보

---

## Slide 08 | Spring Boot 3.5 / Java 21 마이그레이션

[ 이미지: 전환 항목 체크리스트 형태 또는 Before/After 레이어 비교 - javax→jakarta, Security 설정, RestTemplate→WebClient, VM→k8s ]

배경

CRMS 통계 서비스가 EOL 임박한 레거시 환경에서 운영 중.
보안 취약점 대응 기반이 없는 상태.

수행 내용 (단독 수행)

- javax → jakarta 네임스페이스 전환 (전 레이어)
- Spring Security 6 대응: WebSecurityConfigurerAdapter 제거, 람다 기반 DSL로 재작성
- RestTemplate → WebClient 전환 및 외부 연동 재정비
- VM 기반 → Kubernetes(DKOS) 배포 전환: Dockerfile / Vault 설정 / Kustomize 오버레이 정비
- ShedLock 기반 분산 배치 락 적용

결과

- EOL 프레임워크 위험 해소
- 보안 취약점 대응 기반 마련
- Vault 기반 시크릿 관리 및 세션 보안 강화

---

## Slide 09 | CRMS-API 서버 분리 - 독립 배포 구조 전환

[ 이미지: Before / After 서버 구조 - Before: CRMS 단일 서버에 API 혼재 / After: CRMS 본 서버 + CRMS-API 분리 ]

배경

CRMS 규모 확대로 API 기능이 혼재되면서 변경 영향 범위 증가.
하나의 배포 단위에서 기능을 분리하기 어려운 구조.

해결

- RESTful 기반 CRMS-API 전담 서버를 신규 설계 및 점진 이관
- Springdoc OpenAPI 기반 API 문서화 및 표준 응답 규격 / 공통 Exception Handler 정비
- ACL 강화, CORS 정책 재정의, 민감 데이터 암호화 적용

결과

- API 서버 독립 배포로 변경 영향 범위 축소
- CRMS 본 시스템 부하 분산
- 보안 수준 강화 및 협업 커뮤니케이션 비용 절감

기간: 2023.11 ~ 2024.07 | 구성: 4명 | 기여도 40%

---

## Slide 10 | 아키텍처 현대화 - 운영 중단 없는 레거시 개선 전략

[ 이미지: Strangler Fig 패턴 단계별 진행 - 기존 구조에서 도메인 단위로 점진 교체되는 흐름 ]

배경

장기 운영으로 누적된 의존성 과다, 유지보수성 저하, 온보딩 난이도 증가.
운영 중인 서비스를 중단 없이 개선해야 하는 제약.

전략: Strangler Fig 점진 이관

- 변경 영향이 큰 영역부터 순차적으로 리팩토링
- 도메인 경계를 명확히 하고 인터페이스 기반으로 의존성 역전(DIP) 적용
- 테스트 커버리지를 핵심 플로우 중심으로 먼저 확보한 뒤 리팩토링 범위 확장
- DDD Layered Architecture로 재설계, DI 기반 서비스 구조로 전환

결과

- 구조 정리로 변경 영향 범위 축소, 유지보수성 개선
- 회귀 리스크 감소로 배포 안정성 향상
- 온보딩 비용 절감

핵심 판단

레거시 개선은 기술 선택이 아니라 운영 리스크를 통제하는 실행 전략의 문제.

---

## Slide 11 | 보안 강화 - Vault & AES-GCM 암호화 체계

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

## Slide 12 | K-GeoPlatform - ETL 파이프라인 & 대용량 데이터 처리

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

## Slide 13 | 기술 스택 & 핵심 역량

[ 이미지: 기술 스택 시각화 - 분류별 아이콘 또는 그리드 레이아웃 ]

Backend

- Java 21, Spring Boot 3.x, Spring MVC, Spring Security 6
- Spring Batch, Quartz (ETL / 배치)
- Node.js, TypeScript, Express, Socket.io

Database & Messaging

- MySQL, PostgreSQL (PostGIS), Oracle, Tibero
- Redis (캐시, 세션, 분산락)
- RabbitMQ (AMQP)
- 파티션 / 인덱스 설계, 쿼리 튜닝

DevOps & Infra

- Kubernetes, Ingress, HPA
- CI/CD (Jenkins), 배포 전략 (롤링, 카나리, 블루그린)
- Multi IDC / Multi Region 운영 경험

Security

- Vault 기반 시크릿 관리, AES-GCM 암호화
- JWT, ACL, ISMS-P 대응

---

## Slide 14 | 지향점

운영 리스크를 먼저 생각합니다

기능을 빠르게 만드는 것보다, 장애가 났을 때 얼마나 빠르게 원인을 파악하고
영향 범위를 줄일 수 있는지를 먼저 고려합니다.

구조가 설명을 대신합니다

도메인 경계가 명확하고 의존성이 정리된 코드는 문서 없이도 읽힙니다.
설계 판단과 그 근거를 남기는 습관을 유지합니다.

운영과 개발을 함께 봅니다

실서비스 운영 경험을 바탕으로 모니터링, 장애 대응, 배포 전략까지
개발과 운영을 하나의 흐름으로 다룹니다.

---
