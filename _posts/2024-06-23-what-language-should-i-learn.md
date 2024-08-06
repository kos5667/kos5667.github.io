---
layout: post
title:  "나는 어떤 언어를 선택하고 배워야 할까?"
date:   2024-06-23 08:00:00 +0900
excerpt_image: "../assets/images/excerpt-2024-04-23-instructions-mocha.png"
categories: Tech
tags: [DevelopmentMethodology, SoftwareArchitecture, Tech, Java, Javascript, Framework]
allow_publishing: true
---
이 글을 작성하게 된 건 최근 이직을 고려하면서 면접을 보게 되었는데, 하나의 면접 질문이 나에게 굉장히 충격으로 다가왔습니다. 그 이유는 내가 신입 때 면접을 위해 달달 외우고 이후로는 그저 주어진 업무에만 치중하고 있다고 느꼈기 때문입니다.
이 블로그 메인에 종종 서브타이틀로 "知彼知己 百戰百勝 (지피지기 백전백승): 상대를 알고 나를 알면 백 번 싸워도 백 번 이긴다."라는 글귀를 볼 수 있을 것입니다. 무엇이든 알고 쓰는 것과 모르고 쓰는 것은 차이가 있을 것이라 생각됩니다.
모르고 구글링만 해서 복사만 할 줄 아는 카피라이터가 되지 않기 위해 열심히 공부합시다.

## 개발언어의 정의
개발 언어란 컴퓨터 프로그램을 작성하는 데 사용되는 언어를 의미한다. 이러한 언어는 사람과 컴퓨터가 소통할 수 있게 해주는 도구로, 각기 다른 문법과 특성을 가지고 있다.
그리고 개발 언어는 크게 두 가지로 나뉘는데, '**Low level languages**'와 '**High level languages**'로 구분된다.

### 'Low level languages'와 'High level languages' 란?
![](/assets/images/2024-06-23-what-language-should-i-learn-1.png)
**Low languages**는 저급 언어로 기계어와 가까운 언어를 말하며, 하드웨어와 직접 상호작용할 수 있도록 설계된 언어이다.
**High languages**는 고급 언어로 인간이 사용하는 언어와 가까운 언어를 말하며, 인간 친화적인 문법과 추상화를 제공하여 프로그램 작성과 유지보수를 쉽게 만들어주는 언어이다

<table>
    <tr>
        <th style="text-align: center"><strong>특징</strong></th>
        <th>저급 언어 (Low Level Languages)</th>
        <th>고급 언어 (High Level Languages)</th>
    </tr>
    <tr>
        <td style="text-align: center"><strong>추상화 수준</strong></td>
        <td>기계 친화적, 하드웨어와 직접 상호작용</td>
        <td>인간 친화적, 하드웨어로부터 추상화됨</td>
    </tr>
    <tr>
        <td style="text-align: center"><strong>성능 및 효율성</strong></td>
        <td>고성능, 메모리 및 CPU 자원 효율적 사용</td>
        <td>상대적으로 느릴 수 있으나, 개발 생산성 높음</td>
    </tr>
    <tr>
        <td style="text-align: center"><strong>사용 용이성</strong></td>
        <td>작성 및 유지보수가 어려움</td>
        <td>읽기 쉽고 쓰기 쉬움, 유지보수 용이</td>
    </tr>
    <tr>
        <td style="text-align: center"><strong>이식성</strong></td>
        <td>특정 하드웨어에 종속적</td>
        <td>다양한 플랫폼에서 사용 가능</td>
    </tr>
    <tr>
        <td style="text-align: center"><strong>예시</strong></td>
        <td>기계어, 어셈블리어</td>
        <td>Python, Java, C++, JavaScript</td>
    </tr>
    <tr>
        <td style="text-align: center"><strong>장점</strong></td>
        <td>빠른 실행 속도, 하드웨어 자원에 대한 세밀한 제어</td>
        <td>코드 작성 및 유지보수가 용이, 다양한 플랫폼에서 사용 가능</td>
    </tr>
    <tr>
        <td style="text-align: center"><strong>단점</strong></td>
        <td>작성 및 유지보수가 어렵고, 가독성이 낮으며, 이식성이 떨어짐</td>
        <td>저급 언어에 비해 실행 속도가 느릴 수 있고, 하드웨어 자원에 대한 세밀한 제어가 어려움</td>
    </tr>
</table>
## High Level Languages

현재 많은 개발자들이 인간 친화적인 언어 High Level Languages를 사용한다.

많은 High Level Languages들 중에 우리들은 어떤 언어를 선택해야하면 언어별로 용도와 특징을 알아보자.
<table>
    <tr>
        <th>Language</th>
        <th>용도</th>
        <th>특징</th>
        <th>장점</th>
        <th>단점</th>
    </tr>
    <tr>
        <td><strong>Python</strong></td>
        <td>웹 개발, 데이터 분석, 인공지능, 자동화 스크립팅 등</td>
        <td>간결하고 읽기 쉬운 문법, 다목적 사용 가능</td>
        <td>
            <ul>
                <li>풍부한 라이브러리</li>
                <li>높은 생산성</li>
                <li>초보자 친화적</li>
            </ul>
        </td>
        <td>
            <ul>
                <li>상대적으로 느린 실행 속도</li>
                <li>모바일 애플리케이션 개발에 적합하지 않음</li>
                <li>메모리 사용량이 많을 수 있음</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td><strong>JavaScript</strong></td>
        <td>클라이언트 측 및 서버 측 웹 개발, 모바일 앱 개발 (React Native), 데스크탑 앱 개발 (Electron)</td>
        <td>웹 개발에 필수적인 언어</td>
        <td>
            <ul>
                <li>다양한 프레임워크와 라이브러리 (React, Angular, Vue.js)</li>
                <li>비동기 처리 지원</li>
                <li>브라우저 호환성</li>
            </ul>
        </td>
        <td>
            <ul>
                <li>구식 브라우저 호환성 문제</li>
                <li>동적 타이핑으로 인한 오류 발생 가능성</li>
                <li>코드 복잡성 증가 시 유지보수 어려움</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td><strong>Java</strong></td>
        <td>대규모 기업용 애플리케이션, 안드로이드 앱 개발, 서버 측 개발</td>
        <td>플랫폼 독립적인 객체지향 프로그래밍 언어</td>
        <td>
        <ul>
            <li>안정성</li>
            <li>풍부한 라이브러리 및 프레임워크</li>
            <li>강력한 커뮤니티 지원</li>
        </ul>
        </td>
        <td>
        <ul>
            <li>상대적으로 느린 성능</li>
            <li>높은 메모리 사용량</li>
            <li>복잡한 문법</li>
        </ul>
        </td>
    </tr>
    <tr>
        <td><strong>C#</strong></td>
        <td>윈도우 애플리케이션 개발, 게임 개발 (Unity), 웹 애플리케이션 개발</td>
        <td>마이크로소프트의 .NET 프레임워크와 함께 사용하는 객체지향 프로그래밍 언어</td>
        <td>
            <ul>
                <li>강력한 통합 개발 환경(IDE)</li>
                <li>다양한 플랫폼 지원</li>
                <li>생산성 높음</li>
            </ul>
        </td>
        <td>
            <ul>
                <li>윈도우 플랫폼에 최적화됨</li>
                <li>.NET 프레임워크에 대한 의존성</li>
                <li>비교적 높은 메모리 사용</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td><strong>C++</strong></td>
        <td>시스템 소프트웨어, 게임 개발, 성능이 중요한 애플리케이션</td>
        <td>C 언어에 객체지향 개념을 도입한 고성능 프로그래밍 언어</td>
        <td>
            <ul>
                <li>고성능</li>
                <li>하드웨어 제어 가능</li>
                <li>다양한 프로그래밍 패러다임 지원</li>
            </ul>
        </td>
        <td>
            <ul>
                <li>복잡한 문법</li>
                <li>수동 메모리 관리 요구</li>
                <li>높은 학습 곡선</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td><strong>TypeScript</strong></td>
        <td>대규모 자바스크립트 애플리케이션 개발</td>
        <td>JavaScript에 정적 타입을 추가한 언어</td>
        <td>
            <ul>
                <li>코드 가독성 향상</li>
                <li>디버깅 용이</li>
                <li>대규모 프로젝트에서 오류 감소</li>
            </ul>
        </td>
        <td>
            <ul>
                <li>설정과 컴파일 과정 필요</li>
                <li>러닝 커브 존재</li>
                <li>기존 JavaScript 프로젝트와의 통합이 어려울 수 있음</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td><strong>Go (Golang)</strong></td>
        <td>서버 측 개발, 클라우드 네이티브 애플리케이션, 시스템 프로그래밍</td>
        <td>구글에서 개발한 간결하고 효율적인 동시성 지원 프로그래밍 언어</td>
        <td>
            <ul>
                <li>높은 성능</li>
                <li>간단한 문법</li>
                <li>뛰어난 동시성 처리</li>
            </ul>
        </td>
        <td>
            <ul>
                <li>비교적 제한된 표준 라이브러리</li>
                <li>복잡한 객체지향 패러다임 부족</li>
                <li>라이브러리 생태계가 다른 언어보다 덜 성숙</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td><strong>Swift</strong></td>
        <td>iOS, macOS, watchOS, tvOS 애플리케이션 개발</td>
        <td>애플에서 개발한 iOS와 macOS 애플리케이션 개발 언어</td>
        <td>
            <ul>
                <li>빠른 성능</li>
                <li>안전한 문법</li>
                <li>강력한 개발 도구(Xcode)</li>
            </ul>
        </td>
        <td>
            <ul>
                <li>애플 생태계에 종속적</li>
                <li>러닝 커브 존재</li>
                <li>상대적으로 작은 커뮤니티</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td><strong>Kotlin</strong></td>
        <td>안드로이드 앱 개발, 서버 측 개발</td>
        <td>JVM에서 실행되는 현대적 언어, 주로 안드로이드 개발에 사용</td>
        <td>
            <ul>
                <li>간결한 문법</li>
                <li>높은 호환성</li>
                <li>null 안전성</li>
            </ul>
        </td>
        <td>
            <ul>
                <li>컴파일 속도가 느릴 수 있음</li>
                <li>새로운 언어로서의 러닝 커브</li>
                <li>제한된 리소스와 자료</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td><strong>Rust</strong></td>
        <td>시스템 프로그래밍, 웹 어셈블리, 임베디드 시스템</td>
        <td>메모리 안전성과 성능을 모두 제공하는 시스템 프로그래밍 언어</td>
        <td>
            <ul>
                <li>메모리 안전성</li>
                <li>높은 성능</li>
                <li>뛰어난 동시성 지원</li>
            </ul>
        </td>
        <td>
            <ul>
                <li>높은 학습 곡선</li>
                <li>긴 컴파일 시간</li>
                <li>복잡한 문법</li>
            </ul>
        </td>
    </tr>
</table>
## Framework

**프레임워크(Framework)**는 소프트웨어 개발에서 코드 구조와 설계를 표준화하여 개발자가 더 쉽게 애플리케이션을 개발할 수 있도록 돕는 도구입니다.
프레임워크는 특정 기능이나 작업을 처리하는 데 필요한 코드와 규칙의 집합으로 구성되며, 개발자가 일관된 방법으로 문제를 해결할 수 있게 합니다.

### 주요 특징
1. **재사용성**: 프레임워크는 공통적으로 필요한 기능(예: 데이터베이스 연결, 세션 관리)을 미리 구현해 놓아서 개발자는 이를 재사용할 수 있습니다. 이를 통해 중복된 코드를 작성할 필요가 줄어듭니다.
2. **구조와 패턴 제공**: 프레임워크는 애플리케이션의 구조를 정하고, 개발자가 따라야 할 규칙과 디자인 패턴을 제공합니다. 이를 통해 프로젝트의 일관성을 유지할 수 있습니다.
3. **추상화**: 많은 복잡한 작업을 추상화하여 쉽게 사용할 수 있도록 제공합니다. 예를 들어, 데이터베이스 쿼리 작성, 요청 처리 등을 간단한 메소드 호출로 대체할 수 있습니다.
4. **생산성 향상**: 공통 기능을 처리하는 도구와 템플릿을 제공하여 개발자의 생산성을 높이고, 개발 시간과 비용을 절감합니다.
5. **유지보수성**: 일관된 코드 구조와 디자인 패턴 덕분에 코드의 가독성이 높아지고, 유지보수가 쉬워집니다.

### 예시
- **웹 애플리케이션 프레임워크**:
  - **Django (Python)**: 완전한 기능을 갖춘 웹 애플리케이션 프레임워크로, 관리자 인터페이스, ORM(Object-Relational Mapping), URL 라우팅 등을 제공합니다.
  - **Spring (Java)**: 엔터프라이즈급 애플리케이션 개발을 위한 강력한 프레임워크로, 종속성 주입(DI)과 같은 주요 디자인 패턴을 지원합니다.
  - **Ruby on Rails (Ruby)**: 코드 작성 속도를 높이는 데 중점을 둔 프레임워크로, CRUD(생성, 읽기, 업데이트, 삭제) 기능을 자동으로 생성하는 기능을 갖추고 있습니다.
  - **Express (Node.js)**: 경량의 웹 프레임워크로, 웹 애플리케이션과 API를 신속하게 개발할 수 있습니다.
  - **Laravel (PHP)**: 쉽고 우아한 구문을 제공하여 PHP 웹 애플리케이션을 개발하는 데 필요한 많은 기능을 내장하고 있습니다.
- **모바일 애플리케이션 프레임워크**:
  - **React Native**: JavaScript를 사용하여 iOS와 Android 애플리케이션을 동시에 개발할 수 있는 프레임워크.
  - **Flutter**: Google에서 개발한 오픈 소스 UI 프레임워크로, 하나의 코드베이스로 iOS와 Android 애플리케이션을 작성할 수 있습니다.
- **데스크탑 애플리케이션 프레임워크**:
  - **Electron**: JavaScript, HTML, CSS를 사용하여 크로스 플랫폼 데스크탑 애플리케이션을 개발할 수 있는 프레임워크.

### 장점
- **빠른 개발**: 미리 정의된 구조와 모듈을 사용하여 개발 속도가 빨라집니다.
- **안정성**: 검증된 코드와 패턴을 사용함으로써 안정성이 높아집니다.
- **보안**: 프레임워크는 보안 관련 문제를 처리하는 기능을 제공하여, 보안성을 강화할 수 있습니다.

### 단점
- **제한된 유연성**: 프레임워크의 구조나 패턴에 맞춰 개발해야 하므로, 필요한 기능을 구현하는 데 제약이 있을 수 있습니다.
- **학습 곡선**: 새로운 프레임워크를 배우고 익히는 데 시간이 걸릴 수 있습니다.
- **종속성**: 특정 프레임워크에 종속되면, 이를 변경하거나 업그레이드하는 데 어려움이 있을 수 있습니다.

프레임워크는 개발의 생산성을 높이고, 코드의 품질을 보장하며, 일관성을 유지하는 데 중요한 역할을 합니다. 따라서 프로젝트의 요구 사항과 팀의 기술 수준에 맞는 프레임워크를 선택하는 것이 중요합니다.