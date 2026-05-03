# 프로젝트

---

### 카카오 고객센터 상담톡 플랫폼 고도화 및 운영

기간: 2022.07 ~ 현재 | 구성: 1명 | 기여도: 100%

| 항목 | 내용 |
| ---: | :--- |
| 프로젝트 개요 | 카카오 전사 고객 상담을 처리하는 실시간 상담톡 플랫폼의 서버 개발/운영/고도화 전담. Node.js/TypeScript 상담 서버, Spring Boot 수신 서버, Kubernetes 인프라 전반을 담당하며 대규모 실서비스 환경에서 고가용성과 무중단 운영을 지속 개선. |
| 기술 스택 | Node.js / TypeScript, Spring Boot 3.4 / Java 21, Redis, RabbitMQ, Kubernetes, Bucket4j, Vault |
| 문제 해결 | GSLB 트래픽 편중: Multi IDC 도입 후 IDC-A에 트래픽 80% 이상 집중 → DNS 캐싱이 원인임을 파악, Kubernetes 내부 Client Service를 추가해 IPVS 기반 2차 분산으로 균등화 달성 / 배포 구조 개선: Multi-Container Pod(FE+BE 묶음)를 Single-Container Pod로 분리 → 빌드 시간 5~8분에서 FE/BE 각 1분으로 단축, FE Pod 8개 → 2개로 감소 / 분산 Rate Limiting: Kubernetes 다중 Pod 환경에서 사용자별 어뷰징 대응이 불가능한 문제를 Redis + Bucket4j Token Bucket 알고리즘으로 해결. 차단 대신 모니터링 알람을 선택해 정상 사용자 오차단 방지 / 후처리 중복 실행: 상담 종료 후 후처리 작업이 다중 Pod에서 동시에 실행되는 문제를 Redis 분산락(SET NX PX)으로 동일 채팅방 후처리의 동시 실행 제어 / 카테고리 초기화 병목: 재귀 처리를 BFS로 전환해 처리 성능 4배 개선 |
| 성과 | Multi IDC 환경 무중단 운영 구조 확보 / 빌드/배포 시간 단축으로 핫픽스 리드타임 감소 / 정상 사용자 영향 없이 어뷰징 감지/대응 체계 구축 / 카나리/블루그린 배포 운영 기반 확보 / Vault 기반 키 관리와 AES-GCM 암호화 적용으로 서버 간 인증 및 민감정보 보호 모듈 구현 |

---

### 상담톡 코드/아키텍처 현대화 (DDD, TypeScript, 테스트)

기간: 2025.05 ~ 2025.07 | 구성: 1명 | 기여도: 100%

| 항목 | 내용 |
| ---: | :--- |
| 프로젝트 개요 | 3년 이상 장기 운영으로 누적된 기술 부채 해소. 기술 중심 패키지 구조로 한 파일 수정이 무관한 기능까지 영향을 주던 문제를 DDD Layered Architecture 기반으로 재설계. |
| 기술 스택 | Node.js / TypeScript, Jest, DDD Layered Architecture |
| 문제 해결 | 구조 재설계: 기술 중심(controllers/services/repositories) → 도메인 중심(domain/application/infrastructure/interfaces) 패키지로 전환, 변경 영향 범위 명확화 / 의존성 정리: 전역 exports 제거 후 인스턴스 기반 DI 도입, 비대 Service를 Interface 기준으로 분해해 DIP 적용 / 점진 이관: 운영 중단 없이 Strangler Fig 패턴으로 5단계 이관. 리팩토링 전 핵심 플로우 테스트 먼저 확보 → 3개월간 운영 사고 0건 / 비동기 개선: Callback 중첩 제거, async/await 전환, 에러 핸들링 표준화 |
| 성과 | 도메인 단위 책임 분리로 변경 영향 범위 축소, 사이드이펙트 추적 가능 / TypeScript + Jest 도입으로 회귀 리스크 감소 및 배포 안정성 향상 / Node 14 → 20 업그레이드, 평문 Secret 제거로 보안 리스크 해소 / 코드 구조 명확화로 온보딩 비용 절감 |

---

### CRMS 통계 서비스 운영 및 현대화

기간: 2022.09 ~ 현재 | 구성: 1명

| 항목 | 내용 |
| ---: | :--- |
| 프로젝트 개요 | 카카오 고객센터 운영자가 매일 사용하는 통계 조회/배치/Excel 출력 서비스 운영 전담. 통계 수치 정합성 이슈 반복 대응, Spring Boot 3.5 / Java 21 마이그레이션, Kubernetes 배포 전환을 수행. |
| 기술 스택 | Java 21, Spring Boot 3.5, Spring Security 6, MyBatis, JPA, PostgreSQL, ShedLock, Kubernetes, Vault |
| 문제 해결 | Spring Boot 3.5 / Java 21 마이그레이션: EOL 임박한 레거시 환경을 단독으로 업그레이드. javax → jakarta 전환, Spring Security 6 대응(WebSecurityConfigurerAdapter 제거 → 람다 기반 DSL), RestTemplate → WebClient 전환, 외부 연동 재정비까지 전 레이어 일괄 반영 / 통계 배치 정합성: 그룹별 실적/상담원 현황/주간 집계 등 반복 발생하는 수치 불일치를 MyBatis SQL과 서비스 레이어를 병행 추적해 보정. 특정 일자 누락 데이터 및 장기 미처리 문의 복구 로직 추가 / Kubernetes 배포 전환: VM 기반 → DKOS 전환. Dockerfile, Vault 설정, Kustomize 오버레이 일괄 정비 |
| 성과 | Spring Boot 3 / Java 21 전환으로 EOL 프레임워크 위험 해소 및 보안 취약점 대응 기반 마련 / 통계 배치 수치 정합성 확보로 운영 데이터 신뢰도 개선 / Vault 기반 시크릿 관리 및 세션 보안 설정 적용으로 보안성 강화 |

---

### CRMS-API 서버 분리 구축 및 운영

기간: 2023.11 ~ 2024.07 | 구성: 4명 | 기여도: 40%

| 항목 | 내용 |
| ---: | :--- |
| 프로젝트 개요 | CRMS 규모 확대로 API 기능이 혼재되면서 변경 영향 범위가 커지고 배포 복잡도가 증가. RESTful 기반 CRMS-API 전담 서버를 분리 구축해 API 영역을 독립 배포/확장 가능한 구조로 전환. |
| 기술 스택 | Java, Spring Boot 3.2, Spring Security, MyBatis, PostgreSQL, Springdoc OpenAPI, Vault |
| 주요 업무 | RESTful API 서버 신규 설계/구축 및 기존 CRMS 기능 점진 이관 / Springdoc OpenAPI 기반 API 문서화 및 표준 응답 규격/공통 Exception Handler 정비 / ACL 강화, CORS 정책 재정의, 민감 데이터 암호화 적용 |
| 성과 | API 서버 독립 배포로 변경 영향 범위 축소 및 CRMS 본 시스템 부하 분산 / ACL/CORS/암호화 적용으로 보안 수준 강화 / OpenAPI 문서화로 협업 커뮤니케이션 비용 절감 |
