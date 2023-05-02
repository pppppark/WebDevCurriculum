# Quest 18-B. 서비스의 운영: 로깅과 모니터링

## Introduction

- 이번 퀘스트에서는 서비스의 운영을 위해 로그를 스트리밍하는 법에 대해 다루겠습니다.

## Topics

- ElasticSearch
- AWS ElasticSearch Service
- Grafana

## Resources

- [ElasticSearch](https://www.elastic.co/kr/what-is/elasticsearch)
- [ElasticSearch 101](https://www.elastic.co/kr/webinars/getting-started-elasticsearch)
- [Grafana Panels](https://grafana.com/docs/grafana/latest/panels/)

## Checklist

- ElasticSearch는 어떤 DB인가요? 기존의 RDB와 어떻게 다르고 어떤 장단점을 가지고 있나요?
  Elasticsearch는 검색 및 분석용 분산형 오픈소스 RESTful 검색 엔진이다.
  Elasticsearch는 Apache Lucene 라이브러리를 기반으로 하며, 분산된 형태로 클러스터를 구성할 수 있어 대용량 데이터 처리에 적합하다.

  기존의 RDB와의 차이점은 다음과 같다.

  - 스키마 : Elasticsearch는 스키마리스(Schemaless) 데이터 저장 방식을 사용한다. 따라서 데이터를 색인할 때 데이터의 형식을 미리 정하지 않아도 되며, 필드의 추가나 변경도 쉽게 할 수 있다.
  - 색인 방식 : Elasticsearch는 검색을 위해 색인을 생성한다. 이때 색인은 기존의 데이터를 변경하지 않고 새로운 데이터 구조를 생성한다. 이를 통해 기존 데이터의 무결성을 유지할 수 있다.
  - 검색 방식 : Elasticsearch는 전문 검색(Full Text Search)을 지원한다. 이는 RDB의 LIKE 연산과 같은 부분 검색과는 달리, 텍스트에 대한 토큰 분석을 통해 정확한 검색을 수행한다.

  Elasticsearch의 장단점은 다음과 같다.
  장점:

  - 대용량 데이터 처리에 적합한 분산형 구조
  - 실시간 검색, 부분 검색, 전문 검색 등 다양한 검색 기능 제공
  - RESTful API를 지원하여 쉬운 인터페이스 제공
  - 높은 확장성과 가용성 제공

  단점:

  - 데이터의 무결성을 보장하기 위해선 별도의 노력이 필요
  - RDB의 JOIN 연산과 같은 복잡한 쿼리 처리에 취약
  - 트랜잭션 처리와 같은 관계형 DB의 고급 기능 지원이 부족

- AWS의 ElasticSearch Service는 어떤 서비스인가요? ElasticSearch를 직접 설치하거나 elastic.co에서 직접 제공하는 클라우드 서비스와 비교하여 어떤 장단점이 있을까요?
  AWS의 Elasticsearch Service는 AWS에서 ElasticSearch를 호스팅하는 완전 관리형 서비스다. 이 서비스를 사용하면 ElasticSearch 클러스터를 생성하고 관리할 필요 없이, 쉽게 검색, 로그 분석, 데이터 분석, 지리적 데이터 분석 등을 위한 다양한 기능을 사용할 수 있다.

  Elasticsearch를 직접 설치하는 경우에는 직접 서버를 프로비저닝하고, ElasticSearch 클러스터를 설치하고, 필요한 경우 클러스터를 스케일링하고, 클러스터의 상태를 모니터링하고, 클러스터의 성능을 최적화하기 위한 작업을 직접 수행해야한다. 반면 AWS Elasticsearch Service를 사용하는 경우에는 이러한 모든 작업을 AWS가 대신 수행해주므로 운영 부담이 줄어들고 안정적인 서비스를 쉽게 사용할 수 있다.

  AWS Elasticsearch Service의 장점으로는 다음과 같은 것들이 있다.

  - 쉬운 배포 및 관리: 클러스터를 생성하고 관리하는 데 필요한 작업을 최소화하므로, 시간과 비용을 절약할 수 있다.
  - 스케일링: ElasticSearch 클러스터의 용량과 성능을 쉽게 스케일링할 수 있다.
  - 보안: Amazon VPC 내에서 실행되므로 네트워크 보안이 강화된다.
  - 모니터링: AWS에서는 모니터링 및 로깅 도구를 제공하여, 클러스터의 상태를 지속적으로 모니터링할 수 있다.

  하지만, AWS Elasticsearch Service를 사용하는 경우에는 서비스 비용이 발생하고, 일부 기능이나 Elastic.co에서 직접 제공하는 서비스에서 제공하는 기능에 제한이 있을 수 있다. 또한, 클러스터를 직접 관리하는 경우에는 특정 요구사항이나 사용자 정의 설정을 쉽게 적용할 수 있다. 따라서 사용하는 상황과 요구사항에 따라 적절한 서비스를 선택해야한다.

- Grafana의 Panel 형식에는 어떤 것이 있을까요? 로그를 보기에 적합한 판넬은 어떤 형태일까요?

  1. Graph Panel: 시계열 데이터를 그래프로 시각화할 수 있는 패널로, 선 그래프, 막대 그래프, 점 그래프 등 다양한 형태의 그래프를 지원한다.
  2. Singlestat Panel: 하나의 수치 데이터를 표시하는 패널로, 게이지(Gauge), 텍스트(Text), 아이콘(Icon) 등 다양한 형태로 표시할 수 있다.
  3. Table Panel: 테이블 형태로 데이터를 표시하는 패널로, 표의 셀에는 수치, 문자열, 링크 등을 넣을 수 있다.
  4. Heatmap Panel: 히트맵 형태로 데이터를 표시하는 패널로, 값을 색상으로 표현하여 데이터의 밀도와 분포를 파악할 수 있다.
  5. Alert List Panel: 알림 조건에 해당하는 이벤트 목록을 표시하는 패널로, 모니터링 대시보드에서 발생한 알림을 확인할 수 있다.

  로그를 보기에 적합한 패널은 Log Panel다. Log Panel은 로그 데이터를 그래프 형태로 시각화할 수 있으며, 검색 기능과 필터링 기능을 제공하여 로그 데이터를 쉽게 분석할 수 있다. 예를 들어, 로그 메시지의 레벨, 에러 타입, 시간대 등으로 필터링하여 원하는 정보를 추출할 수 있다.

## Quest

- 우리의 웹 서버가 stdout으로 적절한 로그를 남기도록 해 보세요.
- ElasticSearch Service 클러스터를 작은 사양으로 하나 만들고, 도커 컨테이너의 stdout으로 출력된 로그가 ElasticSearch로 스트리밍 되도록 해 보세요.
- Grafana를 이용해 ElasticSearch의 로그를 실시간으로 볼 수 있는 페이지를 만들어 보세요.

## Advanced

- ElasticSearch와 Grafana는 어떤 라이센스로 배포되고 있을까요? AWS와 같은 클라우드 제공자들이 이러한 오픈소스를 서비스화 하는 것을 둘러싼 논란은 어떤 논점일까요?
