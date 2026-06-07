---
description: Vercel 에서 직접 만든거라 신뢰성 높음
---

# React Best Practices

여기서도 Vercel-labs 에서 만든 Agent-skills 중에 해당 스킬 1개만 사용하는 듯 하다

{% embed url="https://github.com/vercel-labs/agent-skills" %}

{% code overflow="wrap" %}
```bash
npx skills add vercel-labs/agent-skills
```
{% endcode %}



{% embed url="https://github.com/vercel-labs/agent-skills/tree/main/skills/react-best-practices" %}

> 현재 열어보고 계신 GitHub 페이지의 react-best-practices는 AI 에이전트와 LLM(대형 언어 모델)이 **React 코드를 작성하거나 수정할 때, 성능과 최적화 관점에서 '세계 최고 수준의 모범 사례(Best Practices)'를 준수할 수 있도록 가이드라인을 제공하는 스킬**입니다. Vercel Labs에서 작성한 이 스킬의 핵심 목적과 작동 방식은 다음과 같습니다.
>
> #### 1. 목적: AI가 짜는 React 코드의 질 향상
>
> AI는 코드를 빠르게 짜지만, 종종 성능 저하를 일으키는 구식 패턴이나 잘못된 컴포넌트 구조를 만들기도 합니다. 이 스킬은 AI에게 **"React 코드를 검토하거나 새로 작성할 때 반드시 이 규칙들을 지켜라"** 하고 주입하는 표준 지침서 역할을 합니다.
>
> #### 2. 가이드라인의 주요 영역 (8대 섹션)
>
> 규칙은 성능 최적화와 관련된 8가지 핵심 분야로 나뉘어 체계적으로 관리됩니다.
>
> * **async- (폭포수 현상 제거):** 데이터 페칭이 순차적으로 일어나 화면 로딩이 느려지는 Waterfall 현상 방지
> * **bundle- (번들 크기 최적화):** 앱의 용량을 줄이기 위한 최적화 기법
> * **server- (서버 사이드 성능):** Next.js 등에서 서버 컴포넌트를 사용할 때의 성능 가이드
> * **client- (클라이언트 데이터 페칭):** 클라이언트 측에서 효율적으로 데이터를 가져오는 방법
> * **rerender- / rendering- (리렌더링 및 렌더링 최적화):** 불필요한 컴포넌트 재실행을 막아 화면 버벅임 해결
> * **js- (자바스크립트 성능):** 순수 자바스크립트 실행 속도 최적화
> * **advanced- (고급 패턴):** 더 복잡한 아키텍처를 위한 베스트 프랙티스
>
> #### 3. 구조화된 규칙 제공 (AGENTS.md)
>
> 각 규칙은 AI가 확실하게 이해할 수 있도록 엄격한 템플릿에 맞춰 작성됩니다.
>
> * **나쁜 예시(Incorrect):** 성능에 문제가 생기는 잘못된 코드 패턴을 명시합니다.
> * **좋은 예시(Correct):** 어떻게 고쳐야 하는지 올바른 코드 패턴을 대조하여 보여줍니다.
> * 이 규칙들은 최종적으로 AGENTS.md라는 하나의 컴파일된 파일로 빌드되어 AI 에이전트의 프롬프트나 지식 베이스(Knowledge)로 주입됩니다.
>
> > 💡 **한 줄 요약** AI 에이전트가 개발자를 도와 React 코드를 작성할 때, 성능 저하나 버그가 없는 **최적의 React 및 Next.js 코드를 만들 수 있도록 교과서 역할을 해주는 AI 전용 지침 스킬**입니다.
