# VPC

## VPC 간 연결 방식

{% embed url="https://sharplee7.tistory.com/132" %}

<figure><img src="../../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

### VPC Peering

<div align="left">

<figure><img src="../../.gitbook/assets/image (20).png" alt="" width="563"><figcaption></figcaption></figure>

</div>

VPC 간 1:1 연결 방식 - 두 VPC 간 하나의 피어링 리소스만 설정 가능 (다중 피어링 불가)

사설 IP 사용 - IP 중복 불가

서로 다른 리전 간에도 사용 가능

IGW(Internet GW) 또는 VGW(Virtual Private GW) 가 필요하지 않음

고가용성 연결

글로벌 AWS 백본에서 트래픽 유지



### AWS Direct Connect 와 VGW (Virtaul Private GateWay)

<img src="../../.gitbook/assets/image (88).png" alt="" data-size="original"><img src="../../.gitbook/assets/image (51).png" alt="" data-size="original">

VGW 는 VPC 와 연결을 원할 때 제공해주는 엔드포인트. Direct Connect 와 함께 사용

\[동일 리전 + 동일 계정] 내의 여러 VPC 가 연결 가능

이 구성은 Site-to-Site VPN 과 함께 사용 가능

#### AWS Direct Connect

<div align="left">

<figure><img src="../../.gitbook/assets/image (111).png" alt="" width="375"><figcaption></figcaption></figure>

</div>

1. 1Gbps or 10Gbps 전용 사설 네트워크 연결 제공
2. 사설 네트워크 연결 간 높은 처리량을 유지해야 하는 경우를 상정하여 설계됨 (일회성 작업엔 부적합)
3. VPN 솔루션에 비해 전송 비용 절감 가능



### DGW (Direct Connect GateWay)

<div align="left">

<figure><img src="../../.gitbook/assets/image (90).png" alt="" width="375"><figcaption></figcaption></figure>

</div>

동일 리전 내 서로 다른 계정 간 VPC 연결

→ VPC 간 연결을 위해 Direct Connect 사용 → Direct Connect 는 VGW 와 연결

\[VPC-A] → \[Direct Connect] → \[Data Center Router] → \[Direct Connect] → \[VPC-B] 형태로 전송





### TGW (Transit GateWay)







