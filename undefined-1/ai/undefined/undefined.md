# 에이전틱 엔지니어링

{% embed url="https://brunch.co.kr/@ghidesigner/418" %}

바이브 코딩 이후, 새로운 패러다임 : 에이전틱 엔지니어링

AI 추론 능력을 바탕으로 _**목표 지향적 자율 에이전트**_&#xB97C; 설계, 개발, 운영

<details>

<summary>원본 </summary>

<figure><img src="../../../.gitbook/assets/image (159).png" alt=""><figcaption></figcaption></figure>

</details>

<figure><img src="../../../.gitbook/assets/image (157).png" alt=""><figcaption></figcaption></figure>

> 에이전틱 엔지니어링 (Agentic Engineering)
>
> &#x20; 핵심 개념: AI 에이전트가 자율적으로 멀티스텝 태스크 실행하는 시스템 설계/구축.
>
> <br>
>
> &#x20; \---
>
> &#x20; 일반 AI vs 에이전틱 AI
>
> 일반 AI
>
> * 질문 → 답변 (1회)
> * 수동적
> * 도구 없음
>
>
>
> 에이전틱 AI
>
> * 목표 → 계획 → 실행 → 검증 (반복)
> * 자율적
> * 도구 사용 (코드실행, 검색, API 호출)
>
>
>
> &#x20; \---
>
> &#x20; 핵심 구성요소
>
> &#x20; 1\. LLM (두뇌)
>
> &#x20; \- 추론, 계획, 결정
>
> &#x20; 2\. 도구 (손)
>
> &#x20; \- 웹 검색, 코드 실행, 파일 읽기/쓰기, API 호출<br>
>
> &#x20; 3\. 메모리
>
> &#x20; \- 단기: 컨텍스트 창
>
> &#x20; \- 장기: 벡터 DB, 파일
>
>
>
> &#x20; 4\. 루프 구조
>
> &#x20; 목표 입력 → 계획 → 도구 실행 → 결과 관찰 → 재계획 → ... → 완료
>
>
>
> &#x20; \---
>
> &#x20; 주요 패턴
>
> &#x20; ReAct — Reasoning + Acting 교차
>
> &#x20; Plan-and-Execute — 먼저 전체 계획, 그다음 실행
>
> &#x20; Multi-Agent — 에이전트들이 협력 (오케스트레이터 + 서브에이전트)
>
> &#x20; Reflection — 자기 결과물 검토 후 개선
>
> <br>
>
> &#x20; \---
>
> &#x20; 실전 과제
>
> &#x20; \- 신뢰성: LLM 중간에 길 잃으면 무한루프
>
> &#x20; \- 비용: 도구 호출 많을수록 비용 폭발
>
> &#x20; \- 컨텍스트 관리: 긴 태스크에서 컨텍스트 창 초과
>
> &#x20; \- 에러 복구: 도구 실패 시 graceful 처리
>
> <br>
>
> &#x20; \---
>
> &#x20; 대표 프레임워크
>
> &#x20; \- LangGraph — 상태 기반 그래프
>
> &#x20; \- CrewAI — 롤 기반 멀티에이전트
>
> &#x20; \- Claude Code — 코드 에이전트 (지금 네가 쓰는 것)
>
> &#x20; \- OpenAI Agents SDK





