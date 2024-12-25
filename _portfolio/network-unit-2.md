---
caption: #what displays in the portfolio grid:
  title: 컴퓨터 네트워크 2단원
  subtitle: 응용 계층
  thumbnail: https://velog.velcdn.com/images/dongchyeon/post/153771cc-610c-4ebd-b451-16ba20f8cb05/image.png
  
#what displays when the item is clicked:
title: 컴퓨터 네트워크 2단원
subtitle: 응용 계층
image: https://velog.velcdn.com/images/dongchyeon/post/153771cc-610c-4ebd-b451-16ba20f8cb05/image.png #main image, can be a link or a file in assets/img/portfolio
---
<img src = "https://velog.velcdn.com/images/dongchyeon/post/153771cc-610c-4ebd-b451-16ba20f8cb05/image.png" width="100%">

## 1. Web Application 개발 언어

익히 알고 있는 HTML, CSS, JAVSCRIPT 가 아닌 다른 언어들을 위주로 조사하였다.

### 1. PHP
PHP(Hypertext Preprocessor)는 서버 측에서 실행되는 서버 사이드 스크립트 언어이다. PHP는 동적 웹 페이지를 생성하괴, 데이터베이스와 상호 작용하며, Web Application를 개발하는 데 사용된다.

장점
<ol>구문이 C와 Java와 유사하여 배우기 쉽다.</ol>
<ol>Windows, Mac OS, Linux 등 다양한 운영체제와 호환된다.</ol>

단점
<ol>해석형 언어이기 때문에 대규모 어플리케이션에서 성능 유지에 어려움이 있을 수 있다.</ol>
<ol>멀티 스레딩을 기본으로 지원해주지 않기 때문에 대규모 동시 작업을 처리하는 능력이 제한된다.</ol>


### 2. JSP
JSP(Java Server Pages)는 Java를 사용하여 Web Application을 개발하기 위한 서버 사이드 스크립트 언어이다. Java를 기반으로 하기 때문에 Java의 모든 기능을 사용할 수 있다.

장점
<ol>Java는 플랫폼 독립적이기 때문에 JSP 또한 플랫폼 독립적이다.</ol>
<ol>Spring 및 Struts와 같은 다른 Java 프레임워크와 쉽게 통합될 수 있다.</ol>

단점
<ol>웹 컨테이너가 Servlet 코드를 생성하고 컴파일해야 하기 때문에 처리 시간이 오래 걸린다.</ol>
<ol>동적 페이지 생성에 중점을 두기 때문에 디자인 유연성이 제한될 수 있다.</ol>

### 3. ASP
상호 작용 가능한 웹 페이지와 Web Application을 만들기 위해 Microsoft에서 개발된 서버 사이트 스크립트 언어이다. ASP 스크립트는 VBScript, JScript, C# 등 다양한 언어를 통해 작성할 수 있다.

장점
<ol>SQL Server, Window Server 및 .NET 프레임워크와 같은 다른 마이크로소프트 기술과 호환성이 좋다.</ol>
<ol>사용자 인증, SQL Injection, XSS 등의 보안 위협에 대한 보호 기능을 제공한다.</ol>

단점
<ol>주로 마이크로소프트 기술과 함께 작동하도록 설계되어 있기 때문에 비 마이크로소프트 플랫폼에서 작업하는 개발자에게는 적합하지 않다.</ol>
<ol>Window Server, SQL Server 등 일부 기능에 들어가는 비용 때문에 경제적이지 않다.</ol>


## 2. Client-Server Architecture의 장단점

클라이언트-서버 구조는 클라이언트 컴퓨터가 서버 컴퓨터로부터 서비스나 리소스를 요청하는 네트워크 구조이다.

장점

1. 중앙 집중 제어: 클라이언트-서버 구조는 서버가 사용자 인증, 액세스 제어 및 데이터 저장을 관리할 수 있도록 중앙 제어가 가능하다. 이는 시스템 관리자가 네트워크를 관리하고 보안을 유지하기 쉽도록 한다.
2. 보안성: 클라이언트-서버 구조는 서버가 보안 정책을 시행하고 사용자 인증 및 액세스를 제어할 수 있으므로 보안 수준이 높다.
3. 데이터 일관성: 클라이언트-서버 구조는  서버가 데이터 저장 및 검색을 관리하기 때문에 데이터 일관성을 비교적 더 잘 보장한다.
4. 운영의 용이성: 파일들이 한 서버에서 관리되기 때문에 필요한 파일을 쉽게 모니터링할 수 있고 액세스할 수 있다.

단점

1. 단일 장애 지점: 클라이언트-서버 아키텍처에는 서버가 단일 장애 지점이 되어 서버가 다운되면 전체 네트워크가 마비된다.
2. 비용: 클라이언트-서버 아키텍처는 구현 및 유지 보수 비용이 비싸다. 서버 하드웨어 및 소프트웨어는 견고하고 신뢰성이 있어야 하며, 시스템 관리자는 네트워크를 관리하기 위한 교육을 받아야 한다.
3. 과부하: 더 많은 클라이언트가 네트워크에 추가될수록 서버가 과부하가 걸려 성능 저하가 발생할 수 있습니다.
4. 네트워크 혼잡: 클라이언트-서버 아키텍처는 네트워크 혼잡에 취약하다. 대량의 클라이언트가 서버에서 동시에 서비스를 요청하면 네트워크가 혼잡해져 응답 시간이 느려질 수 있다.

## 3. P2P Architecture의 장단점

P2P는 "Peer to Peer"의 약어로, Client-Server 구조와 다르게 네트워크 구조의 각 노드와 컴퓨터가 서버와 클라이언트의 역할을 모두 수행할 수 있다.

장점

1. 확장성: P2P는 더 많은 노드를 네트워크에 추가하여 쉽게 확장할 수 있는데 이는 중앙 서버 인프라를 사용해 부하를 처리하는 것보다 많은 수의 사용자 및 트래픽을 처리할 수 있다.
2. 회복력: P2P는 몇몇 노드가 다운되더라도 다른 노드가 부하를 처리하여 네트워크가 계속 작동하고 데이터를 제공할 수 있다.
3. 비용 절감: P2P는 중앙 서버 인프라가 필요하지 않기 때문에 구축 및 유지 비용이 절감된다.
4. 빠른 다운로드 소곧: P2P는 데이터를 여러 노드에서 분산시켜 빠른 다운로드가 가능하다.

단점

1. 보안 위험: P2P는 사용자들이 직접 파일을 공유하기 때문에, 바이러스, 악성 코드 등이 포함된 파일을 다운로드할 가능성이 있다.
2. 중앙 제어의 부재: 중앙에서 집중 제어할 수 없기 때문에 액세스 제어를 시행하거나 모든 노드에서 데이터 일관성을 보장하는 등 네트워크의 관리가 힘들 수 있다.
3. 비효율적인 자원 사용: P2P는 데이터가 여러 노드에 분산되기 때문에 모든 노드에서 최신 데이터 버전을 보장하는 것이 어려울 수 있어 자원이 낭비되고 효율성이 감소할 수 있다.
4. 파일의 불안정성: P2P를 통해 다운로드한 파일은 공유자가 업로드한 파일과 같은 것이 아닐 수 있습니다. 파일이 손상되거나 잘못된 버전일 수도 있습니다.

## 4. 클라우드 컴퓨팅

클라우드 컴퓨팅은 인터넷을 통해 자원을 공유하고 분배함으로써 서비스를 제공하는 컴퓨팅 기술이다.

클라우드 컴퓨팅의 특징은 다음과 같다.

1. 자원 공유: 클라우드 컴퓨팅은 자원을 공유하기 때문에, 여러 사용자가 동시에 자원을 사용할 수 있다.
2. 확장성: 클라우드 컴퓨팅은 필요에 따라 자원을 증가시키거나 감소시킬 수 있으므로, 확장성이 뛰어나다.
3. 유연성: 클라우드 컴퓨팅은 다양한 애플리케이션과 플랫폼에서 사용할 수 있다.
4. 높은 가용성: 클라우드 컴퓨팅은 여러 서버를 사용하기 때문에, 장애 발생 시 다른 서버를 통해 서비스를 제공할 수 있다.

클라우드 컴퓨팅의 제공 형태는 다음과 같다.

1. IaaS(Infrastructure as a Service): 가상 머신, 저장 공간, 네트워크 등의 인프라를 제공한다.
2. PaaS(Platform as a Service): 개발 환경, 데이터베이스, 서버 등의 플랫폼을 제공한다.
3. SaaS(Software as a Service): 이메일, 문서 편집 등의 소프트웨어를 제공한다. (예: 마이크로소프트 오피스 365)

## 5. IPC

Inter-Process Communication의 약자로, 단일 컴퓨터 내 또는 네트워크에서 여러 개의 프로세스 또는 스레드 간에 데이터를 교환하는 것을 의미한다.

IPC의 방법에는 다음과 같은 것들이 있다,

1. 공유 메모리: 프로세스 간에 데이터를 복사하지 않고 공통 메모리 영역을 공유하여 데이터를 교환할 수 있다.
2. 파이프: 파이프로 두 개의 프로세스를 연결하고 하나의 프로세스는 데이터를 쓰기만, 다른 하나는 데이터를 읽게만 할 수 있다.
3. 소켓: 네트워크 소켓 통신을 통해 데이터를 공유하는 방식으로 데이터 교환을 위해 양쪽 PC에서 각각 임의의 포트를 정하고 해당 포트를 통해 데이터를 주고받는 방식이다.
4. 메시지 큐: 버퍼 형태로 존재하며, 보내고자 하는 메시지를 큐에 넣고, 받는 측에서 메시지를 검색하여 처리한다. 파이프와는 다르게 데이터의 흐름이 아닌 메모리 공간이며, 다수의 프로세스간 통신이 가능하다.
5. 메모리 맵: 공유 메모리 영역을 생성하고 파일을 메모리에 맵핑하는 방식으로 사용한다. 각 프로세스는 메모리 맵을 통해 파일에 액세스하거나 데이터를 읽고 쓸 수 았더.
6. 세마포어: 위의 IPC 방법들과는 다르게 데이터 전송을 목적으로 하는 것이 아닌, 프로세스 간 데이터를 동기화하고 보호하는데 목적이 있다.

## 6. TCP/IP 프로토콜

TCP/IP 프로토콜은 인터넷에서 데이터를 전송하기 위한 프로토콜이다. Transmission Control Protocol(TCP)와 Internet Protocol(IP) 두 프로토콜을 결합한 것으로 구성된다.

TCP는 데이터 전송의 신뢰성을 보장하기 위해, 오류 검출 및 재전송, 흐름 제어, 혼잡 제어 등의 기능을 제공한다. 

양쪽 모두 데이터를 주고받을 준비가 됨을 보장하기 위해 3-way handshake 방식을 통해 연결을 설정하며 패킷을 전송할 때 수신 측으로부터 확인 응답이 오기 전까지는 데이터를 계속 전송한다.
또한 패킷 손실이나 중복 전송이 발생할 경우, 패킷의 재전송을 시도하며 흐름 제어 기능을 통해 수신 측이 받을 수 있는 데이터의 양을 제한하고, 혼잡 제어 기능을 통해 네트워크 상황에 따라 패킷 전송 속도를 제어한다.

IP는 데이터 패킷의 라우팅과 전송을 담당하며 각각의 패킷에 목적지와 출발지의 IP 주소를 할당하여 패킷을 전송한다. 데이터 전송 과정에서 패킷의 손실이나 손상을 검사하지만, 복구 기능을 제공하진 않는다.