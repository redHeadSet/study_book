# 복잡한 내부 개발 플랫폼(IDP) 구축 Amazon EKS Blueprint로 시작하기

{% file src="../../../.gitbook/assets/발표자료_복잡한_내부_개발_플랫폼(IDP)_구축_Amazon_EKS_Blueprint로_시작하기.pdf" %}

데브옵스 문화 실천에 관심이 많음

\-> 내부 개발 플랫폼 도입을 검토하고 있음 : 하지만 어렵죠

IDP, 에코시스템, 블루프린트...

IDP 에 대한 관심과 이유,

에코시스템으로 왜 내부 개발 플랫폼으로 사용해야 하는지

블루프린츠 : 소개와 함께 구축하는 방법

\-

IDP?

\-

EC2, RDS 등과 같은 기본 서비스를 이용할 확률이 높음 - 이 단계에서는 데브옵스 팀이 없거나 적을 확률이 높음 : 각 갭라팀은 설정과 운용을 직접 수행하는 경우가 많음

비효율적으로 이용할 확률이 높지만 크게 문제되진 않음

\-

다양한 AWS 서비스를 이용하게 되면서 복잡해짐 - 데브옵스 팀이 중요

보안, 컴플라이언스, 모니터링, ㅂ거버넌스, 비용 등을 데브옵스 팀이 중앙에서 관리하고 처리

각 개발팀이 이용하는 서비스는 팀마다 다르며 AWS 운용방식 또한 팀마다 다름

\-

개발 : 서비스 운용에만 집중하고 싶어함 - 이용 규칙을 챙기기 어려워함

데브옵스 : 개발팀이 많아질수록 서비스 종류와 리소스가 많아짐으로 인해 운영 부담

\-> 내부 개발 플랫폼 대두

\-

서비스 개발, 배포, 모니터링, 보안 등 관리하는 플랫폼 의미

사내에서 직접 개발 & 운용 : 커스터마이징 장점

사내에서 규정한 AWs 규칙을 기반으로 설정되며 자연스럽게 개발자 또한 규정에 따라 이용하게 됨

IDP를 이용한 기술 표준화 목표 달성 가능

self-sevice 형태로 이용. : 데브옵스는 각 개발자들에게 aws 이용 규칙이나 감시할 필요성 감소

데브옵스 조직도  편해짐

\-

\-

\-

EKS 가 IDP에 적합하다 : 그 이유는 EKS 에코시스템

EKS : 쿠버네티스 관리형 서비스

에코시스템 관점 : 업스트림 쿠버네티스 환경을 그대로 제공

쿠버네티스에 적용된 걸 그대로 EKS 에서 활용이 가능하다.

\-

더 나아가 AWS  서비스와의 연동 또한 간편함 : AWS 에코 시스템 & EKS 에코 시스템을 같이 활용 가능

\-

다양한 기술이 존재하는 특징 (computing, net, storage) + (AI/ML, service mesh, ci/cd, security 등)

스케줄러 그룹을 제외한 나머지 그룹들은 aws + kubernetes 서비스가 결합되어 잇음

아마존 eks 가 가지는 장점이다

\-

다양한 고객의 요구조건을 충족시킬 수 있는 장점을 가짐

\-

쿠버네티스를 처음 하면 많은 어려움을 느낌 : 블루프린트를 사용하면 간편하게 확인 가능

\-

\-

블루프린트 특징

1. AWS CDK 또는 테라폼 구성
2. well architected framework \
   운영, 보안, 안전성, 성능효율성, 비용최적화, 지속가능성 = 6개가 well-architected
3. 에코시스템 등에서 이용되는 쿠버네티스 기반 플랫폼 설치 가능
4. 자유로운 설정 기능

\-

다양한 구성 요소...

고려할 요소들이 블루프린트의 작성 요소로 자리잡고 있음

클러스터 프로바ㅣ더는 EKS cluster 설정 : EC2, Fargate 기반의 클러스터 구성 가능

파이프라ㅣㄴ : CD 설정을 도와줌 : git repo 또는 pipeline 등을 사용 - CDK 이용 시에만 가능

에드온 : EKS 에코시스템과 연동

팀 : EKS cluster를 이용하는 조직

클러스터 팀 : 관리자, App 팀 : 특정 namespace 에 해당하는 접근 권한을 가짐

\-

블루프린트 예제

CDK 환경에서 블루프린트 객체에 의해 설정 가능

하나의 객체는 하나의 EKS 클러스터를 의미.

빌더 패턴을 활용하여 같이 설정하도록 함.

파이프라인은 파이프랑니 빌더를 사용하여 호출.

객체 지향적인 방법으로 활용하고 있다는 걸 확인이 가능한 예제였다.

\-

블루프린트의 상세 아키텍처 : EKS Cluster : 높은 고가용성 확보를 위해 멀티 AZ 사용.

\-

손쉽게 배포가 가능하다는 그림...

DEv/Test Account + Production Account 를 각각으로 클러스터를 구성한 그림

운영, 보안적 고려하여 그림과 같은 구성이 일반적이다.

\-

관련 상세 정보는 온라인으로 제공되는 깃북을 통해 확인이 가능하다.

CDK, 테라폼 버전이 별도 존재하고 URL 을 통해 확인이 가능.

두 버전 모두 Getting started 항목을 사용하여 블루프린트를 이용하는 걸 권장한다.

\-

다양한 예제는 패턴 쪽에서 예제를 통해 확인이 가능하며 CDK, 테라폼 가각ㄱ으로 확인이 간으하다.

URL 을 통해 각 예제 확인 가능

\-

몇 가지 내부 개발 플랫폼 예제 제공

첫 째로 서비스매쉬 기반의 예제...

X-ray, Istio 를 이용할 수 있음 - 여기선 Istio 를 사용하여 서비스 매쉬 구성

\-

서버리스 예제...

운영 부담 최소화 목적

\-

Data Processing 및 AI/ML 개발 플랫폼


