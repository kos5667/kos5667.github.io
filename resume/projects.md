# 프로젝트

---

### 카카오 고객센터 상담톡 플랫폼 운영 및 아키텍처 개선

기간: 2022.07 ~ 현재 | 구성: 1명 | 기여도: 100%

개요: 카카오 전사 고객 상담을 처리하는 실시간 상담톡 플랫폼 전담. Spring Boot 기반 수신 서버와 Kubernetes 인프라 전반을 책임지며, Multi IDC 고가용성 구조 설계, 분산 시스템 문제 해결, 레거시 아키텍처 현대화까지 수행. Node.js 상담 서버도 함께 운영.

기술 스택: Spring Boot 3.4 / Java 21, Redis, RabbitMQ, Kubernetes, Bucket4j, Vault, Node.js / TypeScript

주요 업무

- GSLB 트래픽 편중: Multi IDC 도입 후 IDC-A에 트래픽 80% 이상 집중 → DNS 캐싱 원인 파악 후 Kubernetes 내부 Client Service를 추가해 IPVS 기반 2차 분산으로 균등화 달성
- 분산 Rate Limiting: Kubernetes 다중 Pod 환경에서 사용자별 어뷰징 감지를 위해 Redis + Bucket4j Token Bucket 알고리즘 설계, 차단 대신 알람 정책으로 정상 사용자 오차단 방지
- 후처리 중복 실행: 상담 종료 후 다중 Pod 동시 실행 문제를 Redis 분산락(SET NX PX)으로 제어
- 배포 구조 개선: Multi-Container Pod를 Single-Container Pod로 분리해 빌드 시간 5~8분에서 FE/BE 각 1분으로 단축
- 아키텍처 현대화: 기술 중심 패키지를 DDD Layered 구조로 전환, Strangler Fig 5단계 이관으로 운영 중단 없이 완료

성과

- Multi IDC 환경 무중단 운영 구조 확보
- Vault 기반 AES-GCM 암호화로 서버 간 인증 및 민감정보 보호 모듈 구현
- 어뷰징 감지 체계 구축으로 정상 사용자 오차단 0건
- 빌드/배포 시간 단축으로 핫픽스 리드타임 감소
- 카나리/블루그린 배포 운영 기반 확보

---

### CRMS 통계 서비스 운영 및 현대화

기간: 2022.09 ~ 현재 | 구성: 1명

개요: 카카오 고객센터 운영자가 매일 사용하는 통계 조회/배치/Excel 출력 서비스 운영 전담. 통계 수치 정합성 이슈 반복 대응, Spring Boot 3.5 / Java 21 마이그레이션, Kubernetes 배포 전환을 수행.

기술 스택: Java 21, Spring Boot 3.5, Spring Security 6, MyBatis, JPA, PostgreSQL, ShedLock, Kubernetes, Vault

주요 업무

- Spring Boot 3.5 / Java 21 마이그레이션: EOL 임박한 레거시 환경을 단독으로 업그레이드. javax → jakarta 전환, Spring Security 6 대응(WebSecurityConfigurerAdapter 제거 → 람다 기반 DSL), RestTemplate → WebClient 전환, 외부 연동 재정비까지 전 레이어 일괄 반영
- 통계 배치 정합성: 그룹별 실적/상담원 현황/주간 집계 등 반복 발생하는 수치 불일치를 MyBatis SQL과 서비스 레이어를 병행 추적해 보정. 특정 일자 누락 데이터 및 장기 미처리 문의 복구 로직 추가
- Kubernetes 배포 전환: VM 기반 → DKOS 전환. Dockerfile, Vault 설정, Kustomize 오버레이 일괄 정비

성과

- Spring Boot 3 / Java 21 전환으로 EOL 프레임워크 위험 해소 및 보안 취약점 대응 기반 마련
- 통계 배치 수치 정합성 확보로 운영 데이터 신뢰도 개선
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
