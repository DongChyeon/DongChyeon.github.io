---
caption: #what displays in the portfolio grid:
  title: DevOps란?
  subtitle: 현대 IT 환경을 혁신하는 DevOps와 클라우드 서비스의 역할
  thumbnail: https://velog.velcdn.com/images/dongchyeon/post/374ac801-6c7a-4efb-8ae5-be6f5e0b606c/image.jpg
  
#what displays when the item is clicked:
title: DevOps란?
subtitle: 현대 IT 환경을 혁신하는 DevOps와 클라우드 서비스의 역할
image: https://velog.velcdn.com/images/dongchyeon/post/374ac801-6c7a-4efb-8ae5-be6f5e0b606c/image.jpg #main image, can be a link or a file in assets/img/portfolio
---

## 1. DevOps란?
- **개발(Development)과 운영(Operations)의 결합**:
  - 소프트웨어 개발과 IT 운영 간의 협력을 증진하여 **효율적이고 빠른 소프트웨어 배포**를 목표로 함.
- **주요 특징**:
  - **자동화**: CI/CD 파이프라인, 인프라 관리 자동화.
  - **협업**: 개발팀과 운영팀 간의 긴밀한 협력.
  - **지속적인 피드백**: 모니터링과 로그 분석을 통한 개선.
- **이점**:
  - 소프트웨어 개발 주기 단축.
  - 품질 향상과 신속한 배포 가능.
  - 시장 요구에 빠르게 대응.

---

## 2. CI/CD 각 단계별 대표적인 도구 정리

| **단계**            | **목적**                                            | **대표 도구**                                            |
|---------------------|----------------------------------------------------|---------------------------------------------------------|
| **코드 관리**       | 코드 버전 관리 및 협업                              | Git, GitHub, GitLab, Bitbucket                         |
| **CI(지속적 통합)**  | 코드 빌드 및 테스트 자동화                          | Jenkins, CircleCI, Travis CI, GitLab CI/CD, Bamboo     |
| **CD(지속적 배포)**  | 배포 자동화 및 환경 구성                            | Spinnaker, ArgoCD, Flux, Harness                       |
| **컨테이너화**       | 애플리케이션 컨테이너로 패키징                      | Docker, Podman                                         |
| **오케스트레이션**   | 컨테이너 배포, 스케일링 및 관리                     | Kubernetes, Docker Swarm                               |
| **모니터링 및 로깅** | 시스템 성능 및 이벤트 추적                          | Prometheus, Grafana, ELK Stack, Datadog, New Relic     |
| **인프라 관리**      | 인프라의 코드화 및 자동화                          | Terraform, Ansible, Chef, Puppet                       |

---

## 3. 컨테이너란?
- **애플리케이션과 필요한 모든 요소(라이브러리, 설정 파일 등)를 패키징한 독립 실행 환경**:
  - 물리적 서버나 가상 머신과 달리, 가볍고 신속하게 실행 가능.
- **특징**:
  - **독립성**: 애플리케이션 간 간섭 없이 실행.
  - **이식성**: 다양한 환경(개발, 테스트, 운영)에서 동일하게 동작.
  - **경량화**: 가상 머신보다 리소스 소모가 적음.
- **대표적인 도구**: Docker, Podman, LXC.
- **사용 예시**:
  - 마이크로서비스 아키텍처에서 서비스 단위로 컨테이너화.
  - CI/CD 파이프라인에서 빌드와 배포를 일관되게 유지.

---

## 4. IaaS란?
- **Infrastructure as a Service**:
  - 서버, 스토리지, 네트워크 등 물리적/가상 인프라를 클라우드로 제공하는 서비스 모델.
- **특징**:
  - 사용자는 인프라 관리 대신 애플리케이션 배포에 집중 가능.
  - 고도의 유연성 제공: 필요에 따라 자원을 확장/축소 가능.
- **대표적인 IaaS 제공업체**:
  - AWS EC2, Google Compute Engine, Microsoft Azure, OpenStack.
- **사용 예시**:
  - 스타트업이 초기 인프라 비용 절감을 위해 가상 서버 활용.
  - 대규모 데이터 처리나 고성능 컴퓨팅 요구 사항에 적합.

---

## 5. SaaS란?
- **Software as a Service**:
  - 클라우드에서 제공되는 소프트웨어 서비스로, 사용자는 설치 없이 인터넷을 통해 접근 가능.
- **특징**:
  - 사용자는 소프트웨어 설치, 유지보수 부담이 없음.
  - 구독 기반으로 비용 절감 가능.
- **대표적인 SaaS 서비스**:
  - Google Workspace (Gmail, Google Drive), Microsoft 365, Salesforce, Slack.
- **사용 예시**:
  - 기업에서 이메일, 문서 관리, 협업 도구로 SaaS를 활용.
  - CRM 도구로 Salesforce를 사용해 고객 관리.

---