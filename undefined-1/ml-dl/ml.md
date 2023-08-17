# 생활코딩 (ML)

{% embed url="https://www.youtube.com/playlist?list=PLuHgQVnccGMDy5oF7G5WYxLF3NCYhB9H9" %}



* 결정 = 비교 + 선택
  * but, 비교가 쉽지 않은 경우 (ex. 대소관계를 모르거나, 비교할 기준이 너무 많은 경우)
  * 컴퓨터가 나오고 통계가 가능해지면서 인간은 선택만 하면 되는...
  * but, 인간의 영역인 결정을 컴퓨터로 옮겨가고 싶어 함 (스스로 결정)



* 문제를 크고 심각하고 과장
  * 의지 → 환경 → 습관 순서대로 바꿈



* 일 = 꿈 + 능력



{% embed url="https://teachablemachine.withgoogle.com/" %}

학습 후 내보내기를 하면 metadata.json, model.json, weights.bin 파일이 나옴 \[확인 필요]



## 모델

* 사람 기준으로 "판단력"의 개념
* 모델을 만드는 과정 : 학습
* 학습이 잘 되어 좋은 모델이 만들어 진 경우, 좋은 추측을 할 수 있음



위 사이트에서 만든 모델 파일을 아래 사이트에 업로드

{% embed url="https://ml-app.yah.ac/" %}

* Teachable Machine 에서 만든 클래스가 블럭으로 구현되어 있음
* cf. 처리에 필요한 카메라 권한 허용 필요



## 표

* 가로 줄 (행) : instance, observed value, record, example, case ...
* 세로 줄 (열) : feature, attribute, variable, field ...



## 독립 변수와 종속 변수

* 독립 변수 : 원인이 되는 값. 어떤 값에 의해 영향을 받지 않는 값
* 종속 변수 : 결과가 되는 값. 독립 변수들에 의해 영향을 받는 값 - 즉, 독립 변수와 인과 관계가 있음
* 상관 관계 : 변수 간 관계가 있는 경우, 서로 상관이 있다고 함
* 인과 관계 : 변수 간 인과가 있는 경우
  * 모든 인과 관계는 상관 관계다
  * 모든 상관 관계가 인과 관계는 아니다.



## 머신 러닝의 분야

<figure><img src="../../.gitbook/assets/image (48).png" alt=""><figcaption></figcaption></figure>

* 지도 학습 : 문제 + 정답을 비교하여 맞추다보면 익숙해짐
* 비지도 학습 : 무언가에 대한 관찰로 통찰력을 가지게 됨
* 강화 학습 : 학습을 통해 강화되긴 하지만(지도 학습과 비슷하지만), 어떻게 하면 더 좋은 방향을 가지게 되는지에 대해 차이를 둠. (더 좋은 보상에 대해 고민하게 됨)



## 지도 학습

역사와 비슷 : 원인 → 결과

1. 컴퓨터에 데이터 입력 (원인과 결과. 그 동안의 역사, 기록 등)
2. 컴퓨터는 데이터를 분석하여 모델을 만들어 냄.

* 좋은 모델을 만들기 위해서는 더 많은 데이터를 입력해야 할 필요가 있음

cf. 위에서 배운 "손톱을 물어뜯는 상황을 볼 때, 그만하라고 얘기하는 프로그램"의 경우, 지도 학습이다.

* 손톱을 물어뜯는 상황 : 이미지 → 독립 변수
* 이미지를 보고 그것이 손톱을 물어뜯는지, 아닌지를 판별 → 종속 변수



### 분류

추측하고자 하는 것이 숫자가 아닌 경우, 분류로 처리 가능



### 회귀

주로 종속 변수가 숫자인 경우, 회귀를 많이 이용함





## 비지도 학습

탐험적인 학습이라 볼 수 있음

각 변수간 연관을 찾아내고 학습하는 것



### 군집화

비슷한 것을 찾아서 그룹을 만드는 것

cf. 분류와 다른 것은? : 분류는 어떠한 대상을 어떤 그룹에 넣는 것. 군집화는 그 그룹 자체를 만드는 것.

<figure><img src="../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

군집화 모듈에 n 개의 레코드와 m개의 클러스터 수를 입력하면 m개의 클러스터 갯수로 레코드를 분류하여 군집 형성

### 변환

cf. 이 부분은 생활코딩에서 제공하지 않아, 별도로 찾아봐야 할 듯



### 연관 규칙

\= 장바구니 학습 = 추천

ex) 주로 라면을 산 사람이 계란을 산다면 : 라면-계란 간 연관이 있다고 확인이 가능.

but, 주문한 사람이 매우 많고, 품목 또한 매우 많다면 이 제품간 연관 관계를 사람이 파악하기란 불가능에 가까움

→ 연관 관계를 찾아내기 위해 연관 학습을 할 수 있음



<figure><img src="../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

* 레코드 간 연관을 파악하는 것 : 군집화
* 속성 간 연관을 파악하는 것 : 연관규칙



## 강화 학습

지도 학습 : "배움"

강화 학습 : 일단 해보는 "경험"

행동의 결과가 좋다면 상을 받고, 결과가 나쁘면 벌을 받는, 강화 학습의 기본적인 방식

<figure><img src="../../.gitbook/assets/image (57).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (61).png" alt=""><figcaption></figcaption></figure>



## 어떤 머신러닝을 사용해야 할까

<figure><img src="../../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>



