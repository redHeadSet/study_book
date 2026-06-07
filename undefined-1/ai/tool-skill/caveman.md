---
description: '[클로드한테 우가우가 시켰더니 토큰 87% 줄었습니다]'
---

# Caveman

{% embed url="https://youtu.be/iEScgjg_eR4" %}

{% embed url="https://getcaveman.dev/" %}

{% embed url="https://github.com/JuliusBrussee/caveman" %}



## 설치법

```bash
# macOS / Linux / WSL / Git Bash
curl -fsSL https://raw.githubusercontent.com/JuliusBrussee/caveman/main/install.sh | bash

# Windows (PowerShell 5.1+)
irm https://raw.githubusercontent.com/JuliusBrussee/caveman/main/install.ps1 | iex
```

설치 후 Claude code 등에서

```bash
type /caveman or say "talk like caveman". Stop with "normal mode".
```

/caveman 또는 talk like caveman 을 입력해서 활성화시킨다.

> [INSTALL.mdJuliusBrussee/caveman](https://github.com/JuliusBrussee/caveman/blob/main/INSTALL.md)​



***

## 옵션

> Claude Code에서 토큰을 절약하기 위해 사용하는 **Caveman(원시인 모드)** 스킬은 **압축 강도를 3단계로 조절**할 수 있습니다. \[[1](https://news.hada.io/topic?id=28238)]대화창에 아래 명령어를 입력해 강도를 변경해 보세요.
>
> **`/caveman lite` (Lite 모드)**: 자연스러운 문장을 유지하면서 군더더기(인사말 등)만 제거. **`/caveman full` (Full 모드)**: **기본값**입니다. 접속사와 관사를 생략하고 핵심 단어 위주로 요약합니다. **`/caveman ultra` (Ultra 모드)**: 극단적인 압축 모드로, 기호(->)나 약어를 사용하여 텍스트를 최소화합니다.
>
> 이 외에도 `wenyan`(한문식), `precise` 등 추가적인 문체 모드로 전환이 가능합니다.한 번 설정한 모드는 세션이 끝날 때까지 유지되며, 원래의 답변 방식으로 되돌리고 싶다면 `/stop caveman` 또는 `/normal mode`를 입력하시면 됩니다.
>
> Caveman 스킬을 사용할 때 세션 전체의 기본 강도를 고정하고 싶다면 다음 방법을 이용하세요
>
> * **환경 변수 설정** (가장 높은 우선순위): `export CAVEMAN_DEFAULT_MODE=ultra` 입력
> * **설정 파일 수정** (`~/.config/caveman/config.json`): `{ "defaultMode": "lite" }` 추가 \[[1](https://github.com/juliusbrussee/caveman/blob/main/skills/caveman-help/SKILL.md)]caveman을 사용할 때 발생하는 토큰 변화나 환경 설정 방법에 대해 추가로 궁금한 점이 있으신가요? **사용 중인 환경**이나 **원하는 특정 세션 환경**을 알려주시면 가장 알맞은 최적화 방법을 안내해 드리겠습니다.



***

## 코딩 관련

{% embed url="https://github.com/JuliusBrussee/caveman-code" %}

```bash
npm install -g @juliusbrussee/caveman-code
```

