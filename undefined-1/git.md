# Git

## Git 전략

### Git Flow

<figure><img src="../.gitbook/assets/image (44).png" alt="" width="375"><figcaption></figcaption></figure>

#### 브랜치 구성

*   main (master)

    출시 가능한 프로덕션 코드
*   develop

    다음 버전 개발을 위한 코드
*   feature

    하나의 기능 개발을 위한 코드. develop 브랜치에서 파생

    머지하는 경우, Fast-forward 방식이 아닌 merge commit 을 생성하여, 히스토리가 특정 기능 단위로 관리될 수 있도록 함
*   release

    배포 준비 브랜치\
    develop 브랜치에서 파생\
    배포 시, develop 과 main 브랜치 2군데 모두 merge
* hotfix\
  배포된 버전에 문제가 생겼을 때 처리\
  main 브랜치에서 파생\
  배포 시, develop 과 main 브랜치 2군데 모두 merge



#### 한계점 : 웹 어플리케이션에 적합하지 않음

> _Git-Flow는 등장하고 10년 넘게 표준처럼 자리잡고, 더 나아가 마치 만병통치약처럼 사용되었다. 현재는 **Git으로 관리되는 인기있는 유형의 소프트웨어가 웹 어플리케이션으로 이동**하고 있다. **웹 어플리케이션은 일반적으로 롤백되지 않고, 지속적으로 제공(Continuous Delivery)**되므로 **여러 버전의 소프트웨어를 지원할 필요가 없다**._\
>
>
> _웹 어플리케이션은 내가(Vincent Driessen) 10년전 블로그 글을 쓸때에는 염두해둔 소프트웨어 유형이 아니다. **팀이 소프트웨어를 지속적으로 제공**한다면, Git Flow 대신 **Github Flow와 같은 더 단순한 워크플로우**를 채택할 것을 제안한다._\
>
>
> _그러나 명시적으로 버전을 관리해야하는 소프트웨어를 개발한다면, 여전히 Git Flow가 적합할 수 있다._



### Github Flow

<figure><img src="../.gitbook/assets/image (82).png" alt=""><figcaption></figcaption></figure>

#### 브랜치 구성

* main\
  항상 Stable 상태의 브랜치. (= 언제 배포하든 문제가 없고, 새로 만들어도 문제가 없어야 함)\
  이 브랜치의 모든 커밋은 빌드와 테스트를 통과한 상태여야 함
* topic\
  새 기능 개발 시 main 에서 파생\
  feature, hotfix 브랜치와 동일한 역할\
  구체적인 이름으로 네이밍 필요\
  기능이 완성되지 않아도 지속적으로 push (끊임없는 커뮤니케이션)\
  기능 완성 시, Pull Request 를 보내 코드리뷰 후 merge



## 자주 사용하는 명령어 정리

<table><thead><tr><th width="294">command</th><th>description</th></tr></thead><tbody><tr><td>git branch -av</td><td>로컬 및 원격 브랜치 조회</td></tr><tr><td>git branch [new-branch-name]</td><td>새로운 브랜치 생성</td></tr><tr><td>git checkout [branch-name]</td><td>현재 브랜치 변경</td></tr><tr><td>git merge [branch-name]</td><td>현재 브랜치에 다른 브랜치 병합</td></tr><tr><td>git pull</td><td>원격 브랜치 변경사항을 내려받음</td></tr><tr><td>git remote update</td><td>모든 원격 브랜치 변경 사항 확인 (내려받지 않음)</td></tr><tr><td>git fetch</td><td>현재 브랜치의 원격 브랜치 변경 사항 확인 (내려받지 않음)</td></tr></tbody></table>



* git merge --no-ff 옵션

<figure><img src="../.gitbook/assets/image (105).png" alt=""><figcaption></figcaption></figure>

* \-ff : fast-forward 준말로, 병합하려는 브랜치의 커밋 로그들이 그대로 병합되는 브랜치의 커밋 로그처럼 작성되면서 병합
* \--no-ff : 위와 다르게, 병합하려는 브랜치의 커밋 로그는 그대로 남아있는 상태로, 병합되는 브랜치에 새로운 merge 커밋 로그가 생성되면서 병합

cf. --no-ff 옵션을 기본으로 사용

```
git config --global merge.ff no
```



* git pull --ff-only
* 위의 git config --global merge.ff no 옵션 적용 후, git pull 명령을 보내면 pull 명령을 받아 merge 했다는 commit 이 생성됨
* 위 처리가 필요없다면, --rebase 또는 --ff-only 옵션을 주어 처리가 가능
* 참고

{% embed url="https://stackoverflow.com/questions/8509396/git-pull-results-in-extraneous-merge-branch-messages-in-commit-log" %}

cf. --ff-only 옵션을 기본으로 사용

```
git config --global pull.ff only
```



