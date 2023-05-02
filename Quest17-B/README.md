# Quest 17-B. 배포 파이프라인

## Introduction

- 이번 퀘스트에서는 CI/CD 파이프라인이 왜 필요한지, 어떻게 구축할 수 있는지 등에 대해 다룹니다.

## Topics

- Continuous Integration
- Continuous Delivery
- AWS Codebuild

## Resources

- [AWS: Continuous Integration](https://aws.amazon.com/ko/devops/continuous-integration/)
- [AWS: Continuous Delivery](https://aws.amazon.com/ko/devops/continuous-delivery/)
- [AWS Codebuild](https://aws.amazon.com/ko/codebuild/getting-started/)

## Checklist

- CI/CD는 무엇일까요? CI/CD 시스템을 구축하면 어떤 장점이 있을까요?
  CI/CD는 지속적인 통합/배포(Continuous Integration/Continuous Deployment)를 의미한다. 이는 소프트웨어의 개발과 배포를 자동화하여 개발자가 더욱 효율적으로 작업할 수 있도록 돕는 방법이다.
  CI/CD 시스템을 구축하는 가장 큰 장점은 소프트웨어 개발과 배포 과정에서 발생할 수 있는 인적 오류를 줄일 수 있다는 것이다. 이를 통해 소프트웨어 개발 및 배포 과정에서 발생할 수 있는 문제를 최소화하고, 안정적으로 릴리스를 수행할 수 있다. 또한 CI/CD 시스템을 이용하면 개발자들이 변경 사항을 더 빠르게 반영하고 배포할 수 있으며, 배포 주기를 단축시켜 고객에게 빠르게 제품을 제공할 수 있다.
  CI/CD 시스템을 구축하면 자동화된 테스트, 빌드, 배포, 모니터링 등의 작업이 이루어진다. 이를 통해 소프트웨어 개발 과정에서 생산성을 높일 수 있다. 또한, CI/CD 시스템을 통해 개발자들은 빠르게 피드백을 받을 수 있다. 이를 통해 문제점을 빠르게 파악하고 수정할 수 있다.
  CI/CD 시스템은 DevOps를 구현하는 데 있어서 중요한 역할을 한다. 개발자와 운영팀이 협력하여 개발과 배포를 자동화하고, 릴리스 주기를 빠르게 하면서 안정적인 운영을 보장할 수 있다. 이는 기업의 비즈니스 성장에 큰 도움이 된다.

- CI 시스템인 Travis CI, Jenkins, Circle CI, Github Actions, AWS Codebuild 의 차이점과 장단점은 무엇일까요?
  Travis CI, Jenkins, Circle CI, Github Actions, AWS CodeBuild은 모두 CI/CD 파이프라인을 구축하기 위한 도구이다.

  - Travis CI: Travis CI는 클라우드 기반의 분산 CI 서비스로, 오픈 소스 프로젝트에서 무료로 사용할 수 있다. 대부분의 언어와 프레임워크를 지원하며, Github과의 연동이 강점이다. Travis CI는 매우 쉽게 설정하고 사용할 수 있어 개발자들 사이에서 인기가 높다.

  - Jenkins: Jenkins는 오픈 소스 CI/CD 툴로, 매우 유연하고 확장성이 뛰어나다. 다양한 플러그인을 제공하며, 거의 모든 프로젝트 유형과 툴을 지원한다. 그러나 초기 설정이 복잡하고 사용법이 어려울 수 있다.

  - CircleCI: CircleCI는 Travis CI와 유사한 클라우드 기반의 CI/CD 서비스로, 빌드 파이프라인 구성을 매우 쉽게 할 수 있다. 또한, Docker 이미지를 이용한 빌드 및 배포를 지원하며, Github과의 연동이 강점이다.

  - Github Actions: Github Actions는 Github에서 제공하는 CI/CD 도구로, Github 리포지토리와 강력하게 통합되어 있다. 커스텀 스크립트를 사용하여 빌드 및 배포 파이프라인을 쉽게 구성할 수 있다.

  - AWS CodeBuild: AWS CodeBuild는 아마존 웹 서비스(AWS)에서 제공하는 서비스로, 빌드 및 테스트 프로세스를 자동화할 수 있다. AWS 서비스와 쉽게 통합할 수 있다.

  각 도구의 장단점은 다음과 같다.

  - Travis CI: 간편한 설정, Github 연동 지원, 오픈 소스 프로젝트에서 무료 사용 가능
  - Jenkins: 다양한 플러그인 제공, 매우 유연하고 확장성이 높음, 초기 설정이 복잡
  - CircleCI: Docker 이미지 사용 가능, 빌드 파이프라인 구성이 쉬움, Github 연동 지원
  - Github Actions: Github과의 강력한 통합, 커스텀 스크립트 사용 가능
  - AWS CodeBuild: AWS 서비스와 쉽게 통합, 매우 안정적이고 확장성이 높음

## Quest

- AWS Codebuild를 이용하여, 특정 브랜치에 푸시를 하면 린트와 테스트를 거쳐 서버 이미지를 빌드한 뒤, 직전 퀘스트의 EC2 인스턴스에 배포되는 시스템을 만들어 보세요.

## Advanced

- 빅테크 회사들이 코드를 빌드하고 배포하는 시스템은 어떻게 설계되고 운영되고 있을까요?
