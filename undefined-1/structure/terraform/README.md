---
description: https://developer.hashicorp.com/terraform/tutorials/aws-get-started
---

# 테라폼 (terraform)

## 테라폼(terraform)이란



## 테라폼(terraform) 사용법

### 기본 사용법

```shell
# 테라폼 작성 후 ...
# 0. 구성 파일을 HashiCorp 에서 권장하는 스타일로 포맷
terraform fmt

# 1. 초기화 (프로바이더 다운로드, .terraform 폴더 생성)
terraform init

# 2. 계획 확인 (실제 적용 전 미리보기)
terraform plan

# 3. 인프라 생성/변경
terraform apply

# 4. 인프라 삭제
terraform destroy
```

#### terraform fmt

구성 파일을 HashiCorp 에서 권장하는 스타일로 포맷.

#### terraform init

aws 제공자에게서 다운로드하여 현재 디렉토리에 `.terrform` 디렉토리를 만들고, `.terraform.lock.hcl` 파일로 정확한 제공자 버전을 명시하여 실행 간 일관성 보장.

#### terraform validate

구성이 구문적으로 유효하고 일관성 있는지 확인. 리소스 이름 확인이나 지원하지 않는 인수를 참조하면 에러 반환.

정상적인 경우 `Success! The configuration is valid.` 문구 출력

#### terraform plan

변경사항에 대한 실행 계획 생성.&#x20;

<details>

<summary>예시</summary>

```sh
$ terraform plan
data.aws_ami.ubuntu: Reading...
data.aws_ami.ubuntu: Read complete after 1s [id=ami-03aa99ddf5498ceb9]

Terraform used the selected providers to generate the following execution plan. Resource actions are
indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # aws_instance.app_server will be created
  + resource "aws_instance" "app_server" {
      + ami                                  = "ami-03aa99ddf5498ceb9"
      + arn                                  = (known after apply)
      + associate_public_ip_address          = (known after apply)
      + availability_zone                    = (known after apply)
      + cpu_core_count                       = (known after apply)
      + cpu_threads_per_core                 = (known after apply)
      + disable_api_stop                     = (known after apply)
      + disable_api_termination              = (known after apply)
      + ebs_optimized                        = (known after apply)
      + enable_primary_ipv6                  = (known after apply)
      + get_password_data                    = false
      + host_id                              = (known after apply)
      + host_resource_group_arn              = (known after apply)
      + iam_instance_profile                 = (known after apply)
      + id                                   = (known after apply)
      + instance_initiated_shutdown_behavior = (known after apply)
      + instance_lifecycle                   = (known after apply)
      + instance_state                       = (known after apply)
      + instance_type                        = "t2.micro"
      + ipv6_address_count                   = (known after apply)
      + ipv6_addresses                       = (known after apply)
      + key_name                             = (known after apply)
      + monitoring                           = (known after apply)
      + outpost_arn                          = (known after apply)
      + password_data                        = (known after apply)
      + placement_group                      = (known after apply)
      + placement_partition_number           = (known after apply)
      + primary_network_interface_id         = (known after apply)
      + private_dns                          = (known after apply)
      + private_ip                           = (known after apply)
      + public_dns                           = (known after apply)
      + public_ip                            = (known after apply)
      + secondary_private_ips                = (known after apply)
      + security_groups                      = (known after apply)
      + source_dest_check                    = true
      + spot_instance_request_id             = (known after apply)
      + subnet_id                            = (known after apply)
      + tags                                 = {
          + "Name" = "learn-terraform"
        }
      + tags_all                             = {
          + "Name" = "learn-terraform"
        }
      + tenancy                              = (known after apply)
      + user_data                            = (known after apply)
      + user_data_base64                     = (known after apply)
      + user_data_replace_on_change          = false
      + vpc_security_group_ids               = (known after apply)

      + capacity_reservation_specification (known after apply)

      + cpu_options (known after apply)

      + ebs_block_device (known after apply)

      + enclave_options (known after apply)

      + ephemeral_block_device (known after apply)

      + instance_market_options (known after apply)

      + maintenance_options (known after apply)

      + metadata_options (known after apply)

      + network_interface (known after apply)

      + private_dns_name_options (known after apply)

      + root_block_device (known after apply)
    }

Plan: 1 to add, 0 to change, 0 to destroy.

──────────────────────────────────────────────────────────────────────────────────────────────────────────

Note: You didn't use the -out option to save this plan, so Terraform can't guarantee to take exactly these
actions if you run "terraform apply" now.
```

위 예시 상으로 `aws_instance.app_server` 를 생성할 계획을 보여줌

</details>

#### terraform apply

위의 plan 출력 이후 yes 를 입력하면 실제 실행 계획대로 진행

실제 구성을 적용하면 인프라 관련 데이터를 `terraform.tfstate` 파일에 기록함.

#### terraform state list

위의 상태 파일인 `terraform.tfstate` 파일을 보고 테라폼 작업 공간에 있는 리소스와 데이터 소스를 나열.

#### terraform show

데이터 소스가 실제 리소스가 아니더라도 상태 파일에서 이를 추적하여 확인함.

state list 보다 더 자세한 내용을 출력





### 버전 관리

테라폼 자체적인 버전이 있기에 tfenv 사용을 추천 (Claude 및 검색)

```sh
# 테라폼 버전 관리
brew install tfenv

# tfenv 에서 사용하는 내부 모듈인 듯?
brew install grep

# 설치가능한 테라폼 버전 목록 보기
tfenv list-remote

# 설치된 테라폼 버전 보기
tfenv list

# 특정 버전 설치
tfenv install 0.12.9

# 최신 버전 설치
tfenv install latest

# 특정 버전 사용
tfenv use 0.12.9

# 최신 버전 사용
tfenv use latest

# 현재 버전 확인
terraform -version 
```



## 테라폼(terraform) 작성법

### \[terraform] block

{% content-ref url="terraform-block.md" %}
[terraform-block.md](terraform-block.md)
{% endcontent-ref %}

### \[Configuration] blcok

{% content-ref url="configuration-blcok.md" %}
[configuration-blcok.md](configuration-blcok.md)
{% endcontent-ref %}





