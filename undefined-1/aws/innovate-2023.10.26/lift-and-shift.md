# Lift & Shift 로도 가능한 서버리스 전환 : 웹 애플리케이션 편

{% file src="../../../.gitbook/assets/발표자료_Lift_&_Shift_로도_가능한_서버리스_전환___웹_애플리케이션_편.pdf" %}

List and Shift 사용 시에 처음에는 약간 문제가 있을 수 있으나, \
Stangler pattern 을 사용하여 점진적으로 최적화 가능



## 마이그레이션 요구사항

1. 최소 인프라 : 복잡도와 비용
2. 높은 가용성 앱
3. 제로에서 확장과 자동 확장 : 비용
4. 원본 코드 변경 최소화



## 백엔드 구성

일반적으로는 컨테이너 서비스로 확장하는 게 좋음 (위 요구사항에 가장 적합)

<figure><img src="../../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

fargate, app runner -> 제로로 축소되진 않아서 다소 부족함

Lift & shift : 람다 웹 어댑터와 함께 사용하는 게 좋음

### AWS Lambda Web Adapter

source : [https://github.com/awslabs/aws-lambda-web-adapter](https://github.com/awslabs/aws-lambda-web-adapter)

<figure><img src="../../../.gitbook/assets/image (2).png" alt="" width="563"><figcaption></figcaption></figure>

Lambda 에서 오픈소스 프로젝트, 웹앱을 실행하는 도구

* Lambda 런타임 API 및 HTTP API용 일반 어댑터
* 코드 종속성 없음
* 모든 웹 프레임워크 & 프로그래밍 언어 지원
* 기존 도구를 사용하여 로컬에서 개발 & 테스트 가능
* Rust 로 제작되어 안전성과 효율성 제공



### Lambda function URL

<figure><img src="../../../.gitbook/assets/image (4).png" alt="" width="563"><figcaption></figcaption></figure>

Lambda Web Adapter 에서 API를 만드려면? → 아래 3가지 방법

1. API GW
2. Lambda Function URL
3. App Load Balancer

그 중 Lambda Function URL 은 람다 서비스 비용에 포함이라 별도 비용이 발생하지 않음

Lambda 함수를 호출하기 위한 고유 URL 생성

$LATEST 또는 사용자 정의 Alias 가능

<details>

<summary>sample</summary>

<img src="../../../.gitbook/assets/image (8).png" alt="" data-size="original">



</details>



## 프론트 구성

### Amplify

<figure><img src="../../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

<details>

<summary>ref</summary>

[https://docs.amplify.aws/how-amplify-works/#support-matrix](https://docs.amplify.aws/how-amplify-works/#support-matrix)

[https://musma.github.io/2021/09/30/amplify.html](https://musma.github.io/2021/09/30/amplify.html)

[https://github.com/tkang/amplify-forum/blob/main/README\_ko.md](https://github.com/tkang/amplify-forum/blob/main/README\_ko.md)

</details>

<details>

<summary>sample</summary>

![](<../../../.gitbook/assets/image (10).png>)

</details>

## 관리형 DB 구성

<figure><img src="../../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

많은 제품을 지원하지만 mongo DB 예제로 진행

### Mongo Atlas

완전 관리형 데이터베이스 : 몽고 아틀라스 (서버리스 제품)

1. 클러스터 생성
2. 로컬 DB 에서 데이터 전달 (mongodump 명령으로)
3. Atlas 에 데이터 삽입
4. 백엔드 애플리케이션에서 연결 URL 변경

## 보안

### Amazon Cognito

<figure><img src="../../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

Auth 마이그레이션을 위해 사용

다소 코드 변경이 필요한 것으로 확인됨

## 서버리스 스토리지

1. Amazon EFS 사용
2. CloudFront + Amazon S3 사용

두 방법 모두 사용 가능하지만, 예제에서는 2번 방법을 사용



***

## 비용 개선

<figure><img src="../../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

