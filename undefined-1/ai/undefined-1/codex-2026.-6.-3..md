# Codex 는 어떤 형태로 진화하는가 (2026. 6. 3.)

{% embed url="https://youtu.be/H95cVsPJLcw" %}



## 요약 (Gemini)

> 이 영상은 OpenAI의 Replay 2026 행사에서 Dom이 발표한 내용으로, OpenAI가 코딩 AI 모델인 'Codex(코덱스)'를 활용하여 개발 방식을 어떻게 혁신하고 있는지와 AI 기반 개발 시대에 품질 높은 소프트웨어를 배포하기 위한 핵심 전략을 다루고 있습니다.
>
> 주요 내용을 3가지 핵심 요소인 맥락(Context), 검증(Validation), 확인(Verification)으로 나누어 요약해 드립니다.
>
> #### 1. 맥락 (Context) 제공의 중요성
>
> * 코드 생성 병목의 이동: 이제 단순히 코드를 작성하는 것은 AI의 발전으로 더 이상 병목이 아닙니다. 중요한 것은 AI 에이전트가 정확히 일할 수 있도록 올바른 '맥락'을 제공하는 것입니다 \[[01:22](https://www.youtube.com/watch?v=H95cVsPJLcw\&t=82)].
> * 광범위한 도구 연결: OpenAI의 직원 중 80%가 매주 Codex를 사용하며, 개발 환경뿐만 아니라 Slack, Notion, Gmail, Calendar, Figma 등 비개발 시스템까지 모두 연동하여 에이전트가 풍부한 맥락을 파악하도록 합니다 \[[02:54](https://www.youtube.com/watch?v=H95cVsPJLcw\&t=174)], \[[06:55](https://www.youtube.com/watch?v=H95cVsPJLcw\&t=415)].
> * 메모리와 스크린 인식 기능: 최근 실험적 기능인 'Memories(메모리)'와 스크린을 모니터링하여 학습하는 'Chronicle(크로니클)'을 추가하여, 에이전트가 과거의 문제 해결 방식을 기억하고 사용자가 어떤 도구를 쓰는지 스스로 학습할 수 있게 했습니다 \[[10:00](https://www.youtube.com/watch?v=H95cVsPJLcw\&t=600)], \[[10:39](https://www.youtube.com/watch?v=H95cVsPJLcw\&t=639)].
>
> #### 2. 자동화된 검증 (Validation)과 속도
>
> * 에이전트의 자체 검증: Codex는 기존의 컴파일러, 포매터, 린터(Linter) 등의 도구를 활용해 스스로 결과물을 검증하도록 훈련되었습니다 \[[11:35](https://www.youtube.com/watch?v=H95cVsPJLcw\&t=695)].
> * 개발 도구의 속도 혁신: 에이전트가 루프를 돌며 연속적으로 검증 작업을 수행하기 때문에 도구의 처리 속도가 과거보다 훨씬 중요해졌습니다. 이에 따라 OpenAI는 Prettier 대신 Rust 기반의 oxformat을, Typescript 6 대신 Go 기반의 Typescript 7 초기 버전을 도입하는 등 더 빠른 도구로 전환하고 있습니다 \[[12:56](https://www.youtube.com/watch?v=H95cVsPJLcw\&t=776)], \[[13:19](https://www.youtube.com/watch?v=H95cVsPJLcw\&t=799)].
> * 새로운 기능 출시: 발표 당시 기준으로 10분 뒤에 Codex가 백그라운드에서 탭을 띄워 앱을 테스트하고 리서치할 수 있는 Chrome 익스텐션이 출시된다고 발표했습니다 \[[15:14](https://www.youtube.com/watch?v=H95cVsPJLcw\&t=914)].
>
> #### 3. 풀 리퀘스트(PR) 검증 및 확인 (Verification)
>
> * Codex의 코드 리뷰: OpenAI에서 상신되는 모든 pull request(PR)의 100%는 GitHub에 연동된 Codex의 리뷰를 거칩니다. 중요한 이슈 위주로 노이즈 없이 피드백을 주도록 설계되었습니다 \[[16:30](https://www.youtube.com/watch?v=H95cVsPJLcw\&t=990)].
> * 에이전트의 '베이비시팅' 기능: Codex에 PR 링크를 주면 스스로 브랜치를 체크아웃하고, CI 테스트를 모니터링하며, 에러 발생 시 스스로 수정하고 배포 프리뷰(Deploy Preview)가 완료될 때까지 PR을 관리('베이비시팅')합니다 \[[18:50](https://www.youtube.com/watch?v=H95cVsPJLcw\&t=1130)].
> * 코드는 일회성(Disposable)이다: 코드를 작성하는 비용이 그 어느 때보다 낮아졌기 때문에, 특정 코드 라인에 집착하기보다 코드를 언제든 버릴 수 있는 일회성으로 취급하고 제약 조건(Constraints)과 검증 환경을 구축하는 데 집중해야 합니다 \[[23:59](https://www.youtube.com/watch?v=H95cVsPJLcw\&t=1439)].
>
> #### 4. 향후 인공지능 기반 개발의 3대 트렌드
>
> Dom은 앞으로 AI 코딩 에이전트가 나아갈 방향으로 다음 세 가지를 꼽았습니다 \[[24:52](https://www.youtube.com/watch?v=H95cVsPJLcw\&t=1492)]:
>
> 1. 주도성 (Proactivity): 사용자가 매번 명령(프롬프트)하지 않아도 에이전트가 이벤트를 모니터링하고 스스로 알아서 작업을 수행하는 것.
> 2. 독립성 (Independence): 'Chronicle'이나 'Computer Use' 기능을 통해 사람의 밀착 감시 없이도 독립적으로 오랜 시간 과제를 완수하는 것.
> 3. 병렬화 (Parallelization): 로컬 컴퓨터의 한계를 넘어 클라우드 환경(Dev Boxes)을 통해 수많은 에이전트를 동시에 병렬로 실행하는 것.
>
> 관련 영상 링크:
>
> * [OpenAI @ Replay 2026 | OpenAI는 Codex로 개발 방식을 어떻게 바꾸고 있을까요?](http://www.youtube.com/watch?v=H95cVsPJLcw)









