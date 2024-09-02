---
layout: post
title: Network Traffic 분산, Load Balancing
subtitle: SLB, DNS, GSLB에 대한 이론
#excerpt_image: "../assets/images/"
categories: Network
tags: [GSLB, LB, Load Balance, Network, Traffic]
allow_publishing: false
writing: false
---
## Network Traffic 분산 기술 Load Balancing이 왜 필요할까?

1991년 **World Wide Web**의 등장 세계 최초 https://info.cern.ch/hypertext/WWW/TheProject.html 첫 WWW 사이트이며, 1991년 CERN 외부에 공개 되었다고 합니다. 이제 막 인터넷이 보급되기 시작한 시기에는 어떤 사이트가 되었던 인터넷 보급율이 높지 않았기 때문에 Load Balancing에 대한 개념조차 없었던 시기 였습니다. 하지만 1990년대 인터넷이 부상하면서 인터넷 보급율이 올라가고 웹서버의 부상으로 사용자 많아 지면서 웹 서버에 대한 수요가 폭발적으로 증가했습니다. 이와 같은 이유들로 Load Balancing의 중요성이 부각되었습니다.

1990년대에는 웹 서버 로드 밸런싱은 주로 하드웨어 로드 밸런서를 통해 구현퇴었으며, F5 Networks와 같은 기업들이 시장에서 주도적인 역할을 했습니다.

2000년대 이후, 소프트웨어 기반 Load Balancer 기술이 등장했습니다. 소프트웨어 Load Balancer는 하드웨어 Load Balancer 대비 유연성이 높아지고 비용이 저렴해지며 더 큰 인기를 끌었으며, Apache HTTP Server의 mod_proxy_balancer와 같은 오픈 소스 솔루션과 NGINX와 같은 소프트웨어는 고성능 HTTP 서버 및 Load Balancer로 널리 사용되었습니다.

2010년대에는 Cloud Computing이 대두되면서, Load Balancing이 다시 한번 중요한 역할을 하게 되었습니다. AWS, Google Cloud, Microsoft Azure와 같은 Cloud Service는 Load Balancing을 위한 다양한 서비스를 제공하며, 이를 통해 사용자는 탄력적으로 자원을 관리할 수 있게 되었습니다.

Load Balancing은 Network 기술 발전과 함께 꾸준히 진화해 왔으며, 오늘날에는 Server의 가용성, 성능 최적화, 장애 대응 등을 위한 핵심 기술로 자리 잡고 있습니다.
