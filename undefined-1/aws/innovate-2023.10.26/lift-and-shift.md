# Lift & Shift 로도 가능한 서버리스 전환 : 웹 애플리케이션 편

{% file src="../../../.gitbook/assets/발표자료_Lift_&_Shift_로도_가능한_서버리스_전환___웹_애플리케이션_편.pdf" %}

List and Shift 처음에는 약간 문제가 있을 수 있으나 차차 Stangler pattern 을 사용하여 최적화 가능

\-

\-

마이그레이션 요구사항

1. 최소 인프라 : 복잡도와 비용
2. 높은 가용성 앱
3. 제로에서 확장과 자동 확장 : 비용
4. 원본 코드 변경 최소화

\-

mern 스택의 최종 아키텍처...

front : amplify

인증 : cagnito

백엔드 : lambda

\-.-

일반적으로는 컨테이너 서비스로 확장하는 게 좋음

fargate, apprunner -> 이는 제로로 축소되진 않아서 다소 부족함

Lift & shift : 람다 웹 어댑터와 함께 사용하는 게 좋음

\-

AWS Lambda Web Adapter : 오픈소스 프로젝트, 웹앱을 실행하는 도구

\-.-

API 를 만드려면 Lambda Web Adapter 에서 API 를 하려면?

API GW, Lambda Function URL, App Load Balancer 3가지 방법이 있음

\-

Lmaabda function url 은 람다 서비스 비용에 포함이라 별도 비용이 발생하지 않음

\-.-

Amplify : 다양한 클라이언트 라이브러리 제공

\-

React 앱을 마이그레이션 하는 것은 더욱 간단...

\-

완전 관리형 데이터베이스 : 몽고 아틀라스 (서버리스 제품)



