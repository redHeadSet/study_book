---
icon: message-captions
---

# \[terraform] block

### \[terraform] block

{% code title="terraform.tf" lineNumbers="true" %}
```hcl
# 해당 예시는 AWS 를 기준
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.92"
    }
  }
  
  backend "s3" {
    bucket         = "my-terraform-state"
    key            = "production/terraform.tfstate"
    region         = "us-west-2"
    encrypt        = true                # 상태파일 암호화 필수
    dynamodb_table = "terraform-locks"   # 동시성 제어
  }

  required_version = ">= 1.2"
}

# 동시성 제어를 위한 dynamodb 필요
resource "aws_dynamodb_table" "terraform_locks" {
  name         = "terraform-locks"
  billing_mode = "PAY_PER_REQUEST"
  hash_key     = "LockID"

  attribute {
    name = "LockID"
    type = "S"
  }
}
```
{% endcode %}

테라폼 블록은 인프라, 제공자, 버전 등이 포함.

효율적인 프로젝트 관리를 위해 일관된 파일 구조 추천.

#### required\_providers

프로바이더 요구사항 전달

providers 를 통하여 클라우드 공급자의 API 를 호출하여 리소스를 관리.

#### backend

상태파일(terraform.tfstate)을 저장하기 위해 사용

<details>

<summary>설정하지 않을 경우 기본값</summary>

{% code lineNumbers="true" %}
```hcl
terraform {
  backend "local" {
    path = "terraform.tfstate"
  }
}
```
{% endcode %}

다음과 같이 local 영역(현재 디렉토리)에 terraform.tfstate 파일을 자동으로 생성

</details>

#### cf. terraform.tfstate 파일의 역할

현재 인프라의 실제 상태를 기록

다음 plan/apply 시 이 파일을 기준으로 변경사항 계산



<details>

<summary>azure 의 경우</summary>

{% code lineNumbers="true" %}
```hcl
# Configure the Azure provider
terraform {
  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "~> 3.0.2"
    }
  }

  required_version = ">= 1.1.0"
}

provider "azurerm" {
  features {}
}

resource "azurerm_resource_group" "rg" {
  name     = "myTFResourceGroup"
  location = "westus2"
}

```
{% endcode %}

</details>

<details>

<summary>GCP 의 경우</summary>

{% code lineNumbers="true" %}
```hcl
terraform {
  required_providers {
    google = {
      source = "hashicorp/google"
      version = "6.8.0"
    }
  }
}

provider "google" {
  project = "<PROJECT_ID>"
  region  = "us-central1"
  zone    = "us-central1-c"
}

resource "google_compute_network" "vpc_network" {
  name = "terraform-network"
}

```
{% endcode %}

</details>







