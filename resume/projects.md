# 프로젝트

---

### 카카오 고객센터 상담톡 플랫폼 운영 및 아키텍처 개선

기간: 2022.07 ~ 현재 | 구성: 1명 | 기여도: 100%

개요: 카카오 전사 고객 상담을 처리하는 실시간 상담톡 플랫폼 전담. Spring Boot 기반 수신 서버와 Kubernetes 인프라 전반을 책임지며, Multi IDC 고가용성 구조 설계, 분산 시스템 문제 해결, 레거시 아키텍처 현대화까지 수행. Node.js 상담 서버도 함께 운영.

기술 스택: Spring Boot 3.4 / Java 21, MySQL, Redis, RabbitMQ, Kubernetes, Bucket4j, Vault, Node.js / TypeScript / Express / Socket.io

주요 업무

- GSLB 트래픽 편중: Multi IDC 도입 후 IDC-A에 트래픽 80% 이상 집중 → DNS 캐싱 원인 파악 후 Ingress 경로 기반 라우팅과 Kubernetes Service(FE/BE 분리)를 추가해 클러스터 내부 Pod 단위 2차 분산으로 균등화 달성
- 분산 Rate Limiting: Kubernetes 다중 Pod 환경에서 사용자별 어뷰징 감지를 위해 Redis + Bucket4j Token Bucket 알고리즘 설계, 차단 대신 알람 정책으로 정상 사용자 오차단 방지
- 후처리 중복 실행: 상담 종료 후 다중 Pod 동시 실행 문제를 Redis 분산락(SET NX PX)으로 제어
- 배포 구조 개선: Multi-Container Pod를 Single-Container Pod로 분리해 빌드 시간 5~8분에서 FE/BE 각 1분으로 단축
- 아키텍처 현대화: 기술 중심 패키지를 DDD Layered 구조로 전환, Strangler Fig 3단계 이관으로 운영 중단 없이 완료

성과

- Multi IDC 환경 무중단 운영 구조 확보
- Vault 기반 AES-GCM 암호화로 서버 간 인증 및 민감정보 보호 모듈 구현
- 어뷰징 감지 체계 구축으로 정상 사용자 오차단 0건
- 빌드/배포 시간 단축으로 핫픽스 리드타임 감소
- 카나리/블루그린 배포 운영 기반 확보

---

### CRMS 통계 서비스 운영 및 현대화

기간: 2022.09 ~ 현재 | 구성: 1명

개요: 카카오 고객센터 운영자가 매일 사용하는 통계 조회/배치/Excel 출력 서비스 운영 전담. 통계 수치 정합성 이슈 반복 대응, Spring Boot 3.5 / Java 21 마이그레이션, Kubernetes 배포 전환을 수행. 운영자 의사결정과 직결되는 수치 데이터의 정합성을 책임지며, 오류 데이터로 인한 운영 리스크 최소화를 핵심 목표로 삼았다.

기술 스택: Java 21, Spring Boot 3.5, Spring Security 6, MyBatis, JPA, PostgreSQL, ShedLock, Kubernetes, Vault

주요 업무

- Spring Boot 3.5 / Java 21 마이그레이션: EOL 임박한 레거시 환경을 단독으로 업그레이드. javax → jakarta 전환, Spring Security 6 대응(WebSecurityConfigurerAdapter 제거 → 람다 기반 DSL), RestTemplate → WebClient 전환, 외부 연동 재정비까지 전 레이어 일괄 반영
- 통계 배치 정합성: 그룹별 실적/상담원 현황/주간 집계 등 반복 발생하는 수치 불일치를 MyBatis SQL과 서비스 레이어를 병행 추적해 보정. 특정 일자 누락 데이터 및 장기 미처리 문의 복구 로직 추가
- Kubernetes 배포 전환: VM 기반 → DKOS 전환. Dockerfile, Vault 설정, Kustomize 오버레이 일괄 정비

성과

- Spring Boot 3 / Java 21 전환으로 EOL 프레임워크 위험 해소 및 보안 취약점 대응 기반 마련
- 운영자 일별 통계 수치 불일치 반복 발생을 SQL/배치 파이프라인 원인 추적 후 보정 로직 구현, 신뢰 불가 데이터로 인한 운영 판단 오류 리스크 제거
- Vault 기반 시크릿 관리 및 세션 보안 설정 적용으로 보안성 강화

---

### CRMS-API 서버 분리 구축 및 운영

기간: 2023.11 ~ 2024.07 | 구성: 4명 | 기여도: 40%

개요: CRMS 규모 확대로 API 기능이 혼재되면서 변경 영향 범위가 커지고 배포 복잡도가 증가. RESTful 기반 CRMS-API 전담 서버를 분리 구축해 API 영역을 독립 배포/확장 가능한 구조로 전환.

기술 스택: Java, Spring Boot 3.2, Spring Security, MyBatis, PostgreSQL, Springdoc OpenAPI, Vault

주요 업무

- RESTful API 서버 신규 설계/구축 및 기존 CRMS 기능 점진 이관
- Springdoc OpenAPI 기반 API 문서화 및 표준 응답 규격/공통 Exception Handler 정비
- ACL 강화, CORS 정책 재정의, 민감 데이터 암호화 적용

성과

- API 서버 독립 배포로 변경 영향 범위 축소 및 CRMS 본 시스템 부하 분산
- ACL/CORS/암호화 적용으로 보안 수준 강화
- OpenAPI 문서화로 협업 커뮤니케이션 비용 절감

---

### 국토교통부 공간정보 플랫폼 및 공공 행정서비스 개발 (재하정보기술)

기간: 2020.06 ~ 2022.04 | 역할: DaaS팀 파트 담당, SaaS팀 파트장

개요: 국토교통부 K-GeoPlatform 1, 2차 구축 사업 및 정부24 행정서비스 개발에 참여. Spring Batch 기반 ETL 파이프라인 구축, 대용량 공간 데이터 처리 최적화, MSA 기반 서비스 설계를 수행했습니다. 2차 사업에서 SaaS팀 파트장을 맡아 토지대장/비법인/조상땅 찾기 서비스 전반 개발을 주도했습니다.

기술 스택: Java, Spring Boot, Spring Batch, Quartz, MyBatis, PostgreSQL, PostGIS, Oracle, Tibero, Jenkins, Linux

주요 업무

- Spring Batch 및 Quartz 기반 공간/속성 GIS 데이터 ETL 파이프라인 설계 및 구축
- 데이터 전 생애주기 모니터링 현황판 및 DaaS 시스템 개발
- 구 토지대장 대용량 Join 병목을 파티션 테이블 구조 개선으로 해소, PostGIS 공간 쿼리 기반 좌표 처리
- Stored Procedure 기반 ETL 로직 설계, DW/DM 구축 및 Oracle/PostgreSQL/Tibero DB Migration
- 정부24 온종일돌봄 서비스 및 GPKI 행정전자서명 인증 개발
- MSA 아키텍처 기반 서비스 분리 설계 및 RESTful API 문서화

성과

- Spring Batch ETL 구축으로 공간정보 데이터 처리 효율성 향상 및 변동 자료 자동화
- 파티션 구조 개선으로 대용량 Join 쿼리 성능 최적화
- MSA 기반 다수 서비스 독립 배포 구조 확보
- ETL 프로세스 표준화로 데이터 정합성 및 유지보수성 개선
