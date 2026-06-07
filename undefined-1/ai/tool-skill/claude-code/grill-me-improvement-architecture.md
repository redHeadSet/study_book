---
description: mattpocock (type script 권위자라고 함) 이 만든 Skill 목록 중 2가지
---

# Grill Me, Improvement Architecture

## 설치법

{% embed url="https://github.com/mattpocock/skills" %}

{% code overflow="wrap" %}
```bash
npx skills@latest add mattpocock/skills
```
{% endcode %}

원하는 스킬과 에이전트를 선택한 후, `/setup-matt-pocock-skills` 를 반드시 선택

이후 에이전트에서 `/setup-matt-pocock-skills` 를 입력



***

## Grill Me

{% embed url="https://github.com/mattpocock/skills/blob/main/skills/productivity/grill-me/SKILL.md" %}

<div><figure><img src="../../../../.gitbook/assets/image (134).png" alt=""><figcaption></figcaption></figure> <figure><img src="../../../../.gitbook/assets/image (135).png" alt=""><figcaption></figcaption></figure> <figure><img src="../../../../.gitbook/assets/image (136).png" alt=""><figcaption></figcaption></figure></div>

### 개요

> **사용자의 계획이나 디자인(설계)을 철저하게 검증하고 압박 면접하듯 질문을 던져 완벽한 상호 이해에 도달하도록 돕는 스킬**입니다. 사용자가 계획의 허점을 찾고 싶거나, 디자인을 스트레스 테스트(Stress-test)하고 싶을 때 사용하며, 주요 특징은 다음과 같습니다.
>
> * **끊임없는 질문과 검증:** 계획의 모든 측면에 대해 집요하게 질문을 던집니다.
> * **의사결정 트리 해결:** 선택의 기로(Decision tree)마다 얽혀 있는 의존성을 하나씩 해결해 나갑니다.
> * **추천 답변 제공:** 질문을 던질 때마다 AI가 생각하는 추천 답변도 함께 제시합니다.
> * **순차적 진행:** 질문은 한 번에 하나씩만 던져 집중할 수 있게 합니다.
> * **코드베이스 탐색:** 만약 질문에 대한 답을 코드 내에서 찾을 수 있다면, 질문하는 대신 직접 코드베이스를 탐색하여 해결합니다.
>
> > 💡 **한 줄 요약**
> >
> > 사용자가 가져온 기획이나 설계에 대해 AI가 "이 부분은 어떻게 해결할 건가요?"라며 꼬리 질문을 던져, 계획의 빈틈을 메우고 완성도를 높여주는 '끝장 토론' 스킬입니다.



***

## Improvement Architecture

→ 아마 improve-codebase-architecture 로 변경된 듯 하다

{% embed url="https://github.com/mattpocock/skills/blob/main/skills/engineering/improve-codebase-architecture/SKILL.md" %}

<div><figure><img src="../../../../.gitbook/assets/image (137).png" alt=""><figcaption></figcaption></figure> <figure><img src="../../../../.gitbook/assets/image (138).png" alt=""><figcaption></figcaption></figure> <figure><img src="../../../../.gitbook/assets/image (139).png" alt=""><figcaption></figcaption></figure></div>

### 개요

> 현재 열어보고 계신 GitHub 페이지의 improve-codebase-architecture는 **소프트웨어 코드베이스의 구조적 문제를 찾아내고, 코드의 가독성·테스트 가능성·AI 탐색 용이성을 높이도록 아키텍처를 개선하는 스킬**입니다. 이 스킬은 단순히 코드를 깔끔하게 정리하는 것을 넘어, '얕은 모듈(Shallow Module)'을 \*\*'깊은 모듈(Deep Module)'\*\*로 리팩토링하는 데 초점을 맞춥니다. 인터페이스는 단순하지만 내부에 강력한 기능을 숨겨두는 구조를 지향합니다. 작동 프로세스는 크게 3단계로 진행됩니다.
>
> #### 1. 탐색 (Explore)
>
> AI 가 에이전트 도구를 활용해 코드베이스를 유기적으로 분석합니다. 이때 다음과 같은 아키텍처 결함(마찰)을 찾아냅니다.
>
> * 하나의 개념을 이해하기 위해 너무 많은 작은 모듈을 오가야 하는 경우
> * 인터페이스의 복잡도가 내부 구현 코드와 비슷할 정도로 얕은 모듈
> * 강하게 결합되어 결합 부위(Seam) 밖으로 내부 로직이 유출되는 모듈
> * 테스트하기 까다롭거나 테스트가 작성되지 않은 부분
>
> #### 2. 후보군 제시 (Present Candidates)
>
> 발견한 문제점과 개선안을 담은 **독립적인 HTML 리포트**를 생성하여 사용자에게 보여줍니다.
>
> * 리포트에는 어떤 파일이 연관되어 있는지, 현재 구조의 문제점과 해결책, 개선 시 얻을 수 있는 이점이 명시됩니다.
> * 구조를 쉽게 시각화할 수 있도록 **Mermaid 다이어그램을 활용해 개선 전(Before)과 후(After)의 아키텍처**를 나란히 비교해 줍니다.
> * 추천 강도(Strong, Worth exploring, Speculative) 배지를 통해 어떤 리팩토링을 먼저 고려해야 할지 우선순위를 매겨줍니다.
>
> #### 3. 심층 압박 질문 및 조율 (Grilling loop)
>
> 사용자가 리포트에서 개선할 후보를 선택하면, 앞서 언급된 'Grilling' 스킬과 유사하게 **심층 대화(Grilling loop)** 단계로 진입합니다.
>
> * 제약 조건, 의존성 관계, 테스트 생존 여부 등 설계 트리를 꼼꼼하게 짚어갑니다.
> * 대화 중 용어가 명확해지면 프로젝트의 도메인 지식 문서(CONTEXT.md)를 그 자리에서 바로 업데이트합니다.
> * 사용자가 특정 제안을 거절하면, 향후 AI가 같은 제안을 반복하지 않도록 아키텍처 결정 기록(ADR) 문서 작성을 제안하기도 합니다.
>
> > 💡 **한 줄 요약**
> >
> > 복잡하고 꼬여있는 코드 구조를 분석하여 \*\*"더 단순한 인터페이스와 강력한 내부 로직"\*\*을 가진 구조로 개선할 수 있도록, 시각적 리포트를 제공하고 개발자와 1:1 토론을 거쳐 설계를 다듬어주는 아키텍처 리팩토링 전문 스킬입니다.

