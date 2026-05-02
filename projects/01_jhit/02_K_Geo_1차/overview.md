# 클라우드 기반의 공간정보 데이터 통합 및 융복합 활용체계 구축(1차)

## 개요

- **기간:** 2020.06 ~ 2021.03
- **유형:** 회사 프로젝트
- **인원:** 4명
- **역할:** DaaS(데이터 관리 및 활용성 강화)팀 파트 담당자
- **링크:** [K-geop Platform](https://kgeop.go.kr/)

## 프로젝트 소개

> 공간정보 데이터의 통합 관리 및 융복합 활용을 위한 클라우드 기반 플랫폼 구축

공간정보 데이터의 보유·갱신·변동·구축 전 생애주기를 모니터링하고, 데이터 속성·메타정보·이력 등을 통합 관리하는 DaaS(Data as a Service) 시스템을 개발하였습니다. Spring Batch 기반 ETL 파이프라인과 Apache Lucene 검색 엔진을 적용하여 데이터 처리 효율성과 검색 활용성을 강화하였습니다.

## 기술 스택

| 분류 | 기술 |
|-----|-----|
| Backend | Spring Boot, Spring Batch, Quartz, Mybatis, JUnit, Java |
| Frontend | JSP, JavaScript, jQuery |
| Database | PostgreSQL, Oracle, Tibero |
| Infra | Linux, SVN, Jenkins, Gradle |

## 주요 기능

- 데이터 전체 생애주기(보유·갱신·변동·구축) 모니터링 현황판
- DM 및 BI 툴을 활용한 데이터 시각화
- Spring Batch 및 Quartz 스케줄러 기반 데이터 변동 및 ETL 프로세스
- 데이터 속성·메타정보·변동·수집·연관·오류·이력 관리 기능
- 공간 및 속성 데이터 추출 및 제공
- Apache Lucene 검색 엔진을 활용한 속성 데이터 검색 기능
- K-geop Platform PaaS 메인 뷰 데이터 시각화 솔루션

## 내가 기여한 부분

- 데이터 전 생애주기 모니터링 현황판 설계 및 개발
- Spring Batch 및 Quartz 스케줄러를 이용한 ETL 프로세스 설계 및 구축
- DaaS 데이터 속성·메타정보·변동·수집·연관·오류·이력 관리 기능 개발
- 공간 및 속성 데이터 추출·제공 기능 개발
- Apache Lucene 검색 엔진을 사용한 데이터 검색 기능 개발 및 확장
- RDBMS(Oracle, PostgreSQL, Tibero) 비즈니스 데이터 모델링
- TDD 적용을 통한 단위 및 통합 테스트 진행 및 증적 자료 작성
- Linux 기반 웹 애플리케이션 환경 구축 및 운영 관리

## 성과 / 배운 점

- 내부 서비스용 현황판 제공을 통한 융복합 데이터 활용 증진
- Spring Batch 기반 ETL 구축으로 데이터 처리 효율성 향상
- 데이터 다양성 확보 및 개발 이력 관리 체계 마련
- 증적 자료 확보를 통한 개발 과정의 투명성 제고
