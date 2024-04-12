---
layout: post
title:  "What is Docker?"
subtitle: Docker 이론 및 활용
date:   2023-04-12 10:12:00 +0900
excerpt_image: "../assets/images/docker/docker.png"
banner:
  image: "../assets/images/docker/banner-docker.png"
  loop: true
  volume: 0.8
  start_at: 8.5
  opacity: 0.618
  background: "#000"
  height: "100vh"
  min_height: "38vh"
  heading_style: "font-size: 4.25em; font-weight: bold; text-decoration: underline"
  subheading_style: "color: gold"
categories: Docker
tags: [docker]
top: 1
---
> ## **Doc List**
>
> <details>
> <summary><strong>What is Docker?</strong></summary>
> <!-- summary  -->
> 	<ul>
>         <li>1. What is Docker?</li>
>         <li>2. Virtualization(가상화)</li>
>         <li>3. Docker Container</li>
>         <li>4. Docker Architecture</li>
>         <li>5. Docker Engine</li>
>         <li>6. Docker Daemon</li>
>         <li>7. Docker Client</li>
>         <li>8. Docker Registries</li>
>         <li>9. Docker Object</li>
>     </ul>
> </details>
>
> <details>
> <summary><a href="#">Docker doc.</a></summary>
> <!-- summary  -->
> 	<ul>
>         <li>1. Docker lifecycle</li>
>         <li></li>
>     </ul>
> </details>
>
> <details>
> <summary><a href="#">Docker hub</a></summary>
> <!-- summary  -->
> 	<ul>
>         <li>1. Docker lifecycle</li>
>         <li></li>
>     </ul>
> </details>
>
> <details>
> <summary><a href="#">Docker compose</a></summary>
> <!-- summary  -->
> 	<ul>
>         <li>1. Docker lifecycle</li>
>         <li></li>
>     </ul>
> </details>
>
> <details>
> <summary><a href="#">Docker desktop</a></summary>
> <!-- summary  -->
> 	<ul>
>         <li>1. Docker lifecycle</li>
>         <li></li>
>     </ul>
> </details>

## *1. What is Docker?*

![](/assets/images/docker/docker_lxc.png)

### Docker

Docker는 Docker Inc.에 의해 개발 된 Go 언어로 작성된 소프트웨어이며  **LXC라는 컨테이너 기술**을 기반으로 만들어진 상위레벨의 **오픈소스 가상화 플랫폼**입니다. 

**LXC**기술로 만들어진 Docker는 Linux 커널의 여러 기능을 활용하여 기능을 제공하고, 격리 기술들을 사용해 컨테이너로 실행하고 관리할 수 있습니다.

### *LXC(Linux Containers)*

*LXC*(Linux Containers)는 단일 컨트롤 호스트 상에서 여러 개의 고립된 리눅스 시스템 (컨테이너)들을 실행하기 위한 운영 시스템 레벨 **가상화** 방법입니다.

> **가상 머신(Virtual Machine, VM)**
>
> 가상 머신(Virtual Machine, VM)은 물리적 하드웨어 시스템에 구축되어 자체 CPU, 메모리, 네트워크 인터페이스 및 스토리지를 갖추고 가상 컴퓨터 시스템으로 작동하는 가상 환경입니다.
>
> 가상 머신을 사용하는 이유(장점)
>
> - 가상화를 사용하면 데이터를 분할하고 서비스를 서로 다른 서버에서 격리하여 데이터 보안을 강화할 수 있습니다. 각 가상 머신은 호스트 시스템을 포함한 다른 가상 머신과 격리
>
> - 가상 머신은 유지 및 관리가 간편하며 범용성이 뛰어남
> - 하나의 물리적 컴퓨터에서 여러 운영 체제 환경을 실행할 수 있음
>
> 단점
>
> - 하나의 물리적 시스템에서 여러 가상 머신을 실행하면 성능이 불안정해질 수 있음
> - 가상 머신은 물리적 컴퓨터보다 효율성이 떨어지며 실행 속도도 느림 <br/>
>   ex)  *MVC* (Model-View-Controller) Pattern을 구축하여 이를 개발 서버에 배포할 때에는 가상머신을 이용하여 개발 서버를 구축하지만 이를 상용화할 때는 별도에 하트웨어를 구축하여 운영서버를 구축한다.



## 2. Virtualization(가상화)

### 가상화 개념

![](/assets/images/docker/virtualization.png)

가상화는 소프트웨어를 사용하여 프로세서, 메모리, 스토리지 등과 같은 단일 컴퓨터의 하드웨어 요소를 일반적으로 가상 머신(VM)이라고 하는 다수의 가상 컴퓨터로 분할할 수 있도록 해주는 컴퓨터 하드웨어 상의 추상화 계층을 구축합니다. 곧 가상화란 물리적인(HW)를 논리적 객체로 추상화 하는 것.

> **wikipedia**
>
> 컴퓨터에서 컴퓨터 리소스의 추상화를 일컫는 광범위한 용어이다. "물리적인 컴퓨터 리소스의 특징을 다른 시스템, 응용 프로그램, 최종 사용자들이 리소스와 상호 작용하는 방식으로부터 감추는 기술"로 정의할 수 있다.



## 3. Docker Container

![](/assets/images/docker/container.png)

### Container

컨테이너는 가상화 기술 중 하나로 대표적으로 LXC(Linux Container)가 있습니다. 기존 **<u>OS를 가상화</u>** 시키던 것과 달리 컨테이너는 OS레벨의 가상화로 격리된 공간에서 프로세스가 동작하는 기술입니다.

**Docker VS VM(Virtual Machine)**

![](/assets/images/docker/vm.png)

**Docker Container**

컨테이너는 코드와 종속성을 함께 패키징하는 앱 계층의 추상화입니다. 여러 컨테이너가 동일한 시스템에서 실행되고 OS 커널을 다른 컨테이너와 공유할 수 있으며, 각각은 사용자 공간에서 격리된 프로세스로 실행됩니다. 컨테이너는 VM보다 공간을 덜 차지하며(컨테이너 이미지는 일반적으로 수십 MB 크기), 더 많은 애플리케이션을 처리할 수 있으며 더 적은 수의 VM 및 운영 체제가 필요합니다.

**Virtual Machines (VMs)**

가상 머신(VM)은 하나의 서버를 여러 서버로 바꾸는 물리적 하드웨어의 추상화입니다. 하이퍼바이저를 사용하면 단일 시스템에서 여러 VM을 실행할 수 있습니다. 각 VM에는 운영 체제, 애플리케이션, 필요한 바이너리 및 라이브러리의 전체 복사본이 포함되어 있으며 수십 GB를 차지합니다. VM은 부팅 속도가 느릴 수도 있습니다.

|                       | Docker                                                       | Virtual Machines (VMs)                                       |
| --------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **시작 시간**         | 몇 초 안에 부팅됩니다.                                       | VM이 부팅되는 데 몇 분 정도 걸립니다.                        |
| **Runs on**           | Docker는 Docker engine을 사용합니다.                         | VM은 하이퍼바이저를 사용합니다.                              |
| **Memory Efficiency** | 가상화에 공간이 필요하지 않으므로 메모리가 적습니다.         | 표면을 시작하기 전에 전체 OS를 로드해야 하므로 효율성이 떨어집니다. |
| **Isolation**         | 격리 시스템에 대한 조항이 없기 때문에 역경에 빠지기 쉽습니다. | 효율적인 격리 메커니즘으로 인해 간섭 가능성이 최소화됩니다.  |
| **배포**              | 컨테이너화된 단일 이미지만 모든 플랫폼에서 사용할 수 있으므로 배포가 쉽습니다. | 별도의 인스턴스가 실행을 담당하므로 배포 시간이 비교적 오래 걸립니다. |
| **Usage**             | Docker has a complex usage mechanism consisting of both third party and docker managed tools. | Tools are e                                                  |
| 리소스 사용량         | 리소스 사용량 감소                                           | 더 많은 리소스 사용량                                        |
| Guest OS              | 호스트 OS 와 동일한 OS                                       | Windows/Linux 등 다양한 선택 가능                            |
| 이식성                | 컨테이너 이미지 그대로 사용 가능                             | 대부분 가상 이미지에 대한 변환이 필요함                      |

### Docker Image

*이미지* 는 Docker 컨테이너 생성 지침이 포함된 읽기 전용 템플릿입니다 . 

종종 이미지는 몇 가지 추가 사용자 정의와 함께 다른 이미지 를 *기반으로 합니다.* 예를 들어 이미지를 기반으로 하는 이미지를 빌드할 수 `ubuntu` 있지만 Apache 웹 서버와 애플리케이션을 설치하고 애플리케이션을 실행하는 데 필요한 구성 세부 정보를 설치할 수 있습니다.

- 이미지는 컨테이너 실행에 필요한 파일과 설정값들을 포함
- 이미지를 실행한 상태(run)가 컨테이너
- 이미지는 변하지 않음(Immutable)
- Docker Hub에서 pull 하거나 Dockerfile을 build 하여 이미지 생성



## 4. Docker architecture

Docker는 **Client - Server architecture**를 사용합니다. 

Docker *클라이언트* 는 Docker 컨테이너를 빌드, 실행 및 배포하는 무거운 작업을 수행 하는 Docker *데몬 과 통신합니다.* Docker 클라이언트와 데몬 *은* 동일한 시스템에서 실행되거나 Docker 클라이언트를 원격 Docker 데몬에 연결할 수 있습니다.

Docker 클라이언트와 데몬은 UNIX 소켓 또는 네트워크 인터페이스를 통해 REST API를 사용하여 통신합니다. 또 다른 Docker Client는 컨테이너 세트로 구성된 애플리케이션으로 작업할 수 있는 Docker Compose입니다.

![](/assets/images/docker/docker-architecture.png)

## 5. Docker LifeCycle





## 6. Docker engine

Docker Engine(`docker`)는 사용자의 컴퓨터에 설치하여 컨테이너를 build 하고 run 하는 데 사용하는 소프트웨어



## 7. Docker daemon

Docker daemon( `dockerd`)은 Docker API 요청을 수신하고 이미지, 컨테이너, 네트워크 및 볼륨과 같은 Docker 객체를 관리합니다. 

데몬은 Docker 서비스를 관리하기 위해 다른 데몬과 통신할 수도 있습니다.



## 8. Docker client

Docker client( `docker`)는 도커 서버와 통신하기 위한 가장 주요한 기능을 수행합니다. 

예를 들어, docker run 명령어를 실행하면 도커 클라이언트는 해당 명령어를 REST API Call으로 변환하여 도커 데몬(`dockerd`)로 전송합니다.



## 9. Docker registries

Docker registries 는 Docker 이미지를 저장합니다. Docker Hub는 누구나 사용할 수 있는 공개 레지스트리이며 Docker는 기본적으로 Docker Hub에서 이미지를 찾도록 구성되어 있습니다.



## 10. Docker objects

Docker를 사용하면 이미지, 컨테이너, 네트워크, 볼륨, 플러그인 및 기타 개체를 만들고 사용하게 됩니다. 이 섹션은 이러한 개체 중 일부에 대한 간략한 개요입니다.



> ## Reference
>
> https://www.docker.com
>
> https://linuxcontainers.org/lxc/introduction/
>
> https://www.redhat.com/en/topics/virtualization