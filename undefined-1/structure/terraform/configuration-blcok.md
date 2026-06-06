---
icon: abacus
---

# \[Configuration] blcok

### \[Configuration] blcok

{% code title="main.tf" lineNumbers="true" %}
```hcl
provider "aws" {
  region = "us-west-2"
}

data "aws_ami" "ubuntu" {
  most_recent = true

  filter {
    name = "name"
    values = ["ubuntu/images/hvm-ssd-gp3/ubuntu-noble-24.04-amd64-server-*"]
  }

  owners = ["099720109477"] # Canonical
}

resource "aws_instance" "app_server" {
  ami           = data.aws_ami.ubuntu.id
  instance_type = "t2.micro"

  tags = {
    Name = "learn-terraform"
  }
}

```
{% endcode %}

기본적으로 새로운 terraform 블록 생성 시 공급자 블록 및 기본 인프라 정의.

* 1\~3 : provider : 공급자 구성
  * 리소스가 적용되는 옵션 값 지정.&#x20;
  * privider 의 이름은 위의 terraform.tf 에 지정한 이름과 일치.
  * AWS 제공자의 경우, AWS CLI 와 동일 인증 방법을 사용. (aws configure)
    * cf. [https://registry.terraform.io/providers/hashicorp/aws/latest/docs?product\_intent=terraform#environment-variables](https://registry.terraform.io/providers/hashicorp/aws/latest/docs?product_intent=terraform#environment-variables)
* 5\~14 : data : 데이터 소스
  * 클라우드 제공업체의 다른 리소스에 대한 정보 쿼리
  * filter 항목에 일치하는 최신 AWS AMI 정보를 가져옴
  * 위 예시의 data 에 접근하기 위해서는 `data.aws_ami.ubuntu` 로 접근
    * aws\_ami 는 데이터 소스의 타입
    * ubuntu 는 개발자가 정한 별칭
* 16\~23 : resource : 실제 인프라 구성 요소
  * 해당 예시에서는 EC2 생성
  * 예시에서는 t2.micro 인스턴스 생성 및 인스턴스 이름을 "learn-terraform" 으로 생성
  * 왜 .id 라는 값이 붙는가?
    * 실제 data source 는 반환하는 정보가 많음.
      * id : AMI ID
      * name : AMI 이름
      * description : AMI 설명
      * architecture : 아키텍처 (x86\_64 등)
      * creation\_date : 생성 날짜
      * owner\_id : 소유자 ID



### 변수

{% code title="variable.tf" lineNumbers="true" %}
```hcl
variable "instance_name" {
  description = "Value of the EC2 instance's Name tag."
  type        = string
  default     = "learn-terraform"
}

variable "instance_type" {
  description = "The EC2 instance's type."
  type        = string
  default     = "t2.micro"
}

```
{% endcode %}

