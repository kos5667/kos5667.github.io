---
layout: post
title:  "메세지 지향 미들웨어(MOM:Message Oriented Middleware)"
subtitle: Message Oriented Middleware 이론
date:   2024-04-14 16:45:00 +0900
excerpt_image: "../assets/images/excerpt-image-2024-04-14-message-oriented-middleware.png"
categories: Architecture
tags: [MessageOrientedMiddleware, MOM, SoftwareArchitecture, DataSynchronization, AsynchronousCommunication]
---
메시지 지향 미들웨어(Message Oriented Middleware, MOM)는 서로 다른 시스템이나 애플리케이션 간의 메시지 교환을 용이하게 해주는 소프트웨어 또는 하드웨어 인프라입니다. 이를 통해 개발자들은 다양한 네트워크와 플랫폼 환경에서도 각 애플리케이션 간의 통신을 원활하게 할 수 있습니다.

### 1. MOM의 기본 개념

MOM은 비동기 메시지 교환을 지원하여, 한 프로그램이 메시지를 보내고 계속 다른 작업을 수행할 수 있게 합니다. 받는 프로그램은 메시지를 받을 준비가 되었을 때 처리할 수 있습니다. 이 방식은 시스템 간의 결합도를 낮추고, 서로의 프로세스 상태에 영향을 받지 않도록 도와줍니다.

### 2. 주요 특징

- **비동기성**: 메시지 발신자와 수신자가 메시지를 주고받을 때 서로를 기다리지 않아도 됩니다. 이는 시스템의 전반적인 처리능력과 반응성을 향상시킵니다.
- **탈중앙화**: 중앙 서버에 의존하지 않고, 여러 노드가 메시지를 교환할 수 있는 구조를 가지고 있습니다.
- **신뢰성**: 메시지는 안전하게 전송되어야 하며, 전송 중 손실되거나 중복되지 않도록 관리됩니다.
- **확장성**: 시스템을 확장하거나 수정할 때 추가적인 구성 변경 없이도 쉽게 적용할 수 있습니다.

### 3. MOM의 구성 요소

- **Message Queues**: 메시지 큐는 발신자와 수신자 사이에서 메시지를 임시로 저장하는 역할을 합니다. 이 큐를 통해 메시지는 순차적으로 처리될 수 있습니다.
- **Channels**: 채널은 메시지가 전송되는 경로를 정의합니다. 각 채널은 특정 유형의 데이터 또는 특정 서비스와 관련될 수 있습니다.
- **Message Agents**: 메시지 에이전트는 메시지의 라우팅, 변환, 보안 등을 관리합니다.

### 4. 사용 사례

- **시스템 통합**: 서로 다른 기술을 사용하는 시스템들을 통합하는 데 사용됩니다.
- **데이터 동기화**: 분산된 데이터베이스 간에 데이터를 동기화하는 데 사용됩니다.
- **비동기 처리**: 고성능을 요구하는 애플리케이션에서 비동기적으로 데이터를 처리할 필요가 있을 때 유용합니다.

### 5. 대표적인 MOM 제품

- **Apache Kafka**: 대용량의 실시간 데이터 처리에 적합하며, 높은 처리량과 확장성을 자랑합니다.
- **RabbitMQ**: 경량 메시징 시스템으로, 여러 언어와 플랫폼을 지원하며, 다양한 메시징 패턴을 제공합니다.
- **ActiveMQ**: 다양한 프로토콜과 언어를 지원하며, 큐와 토픽 모두를 사용하는 유연성을 제공합니다.