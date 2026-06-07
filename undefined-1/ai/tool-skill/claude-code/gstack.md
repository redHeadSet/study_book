# GStack

{% embed url="https://github.com/garrytan/gstack" %}

설치법이 좀 특이함. Claude code 에 다음과 같이 작성

{% code overflow="wrap" %}
```
Install gstack: run git clone --single-branch --depth 1 https://github.com/garrytan/gstack.git ~/.claude/skills/gstack && cd ~/.claude/skills/gstack && ./setup then add a "gstack" section to CLAUDE.md that says to use the /browse skill from gstack for all web browsing, never use mcp__claude-in-chrome__* tools, and lists the available skills: /office-hours, /plan-ceo-review, /plan-eng-review, /plan-design-review, /design-consultation, /design-shotgun, /design-html, /review, /ship, /land-and-deploy, /canary, /benchmark, /browse, /connect-chrome, /qa, /qa-only, /design-review, /setup-browser-cookies, /setup-deploy, /setup-gbrain, /retro, /investigate, /document-release, /document-generate, /codex, /cso, /autoplan, /plan-devex-review, /devex-review, /careful, /freeze, /guard, /unfreeze, /gstack-upgrade, /learn. Then ask the user if they also want to add gstack to the current project so teammates get it.
```
{% endcode %}

\+ 팀 모드인 경우 다음과 같이 실행

{% code overflow="wrap" %}
```
(cd ~/.claude/skills/gstack && ./setup --team) && ~/.claude/skills/gstack/bin/gstack-team-init required && git add .claude/ CLAUDE.md && git commit -m "require gstack for AI-assisted work"
```
{% endcode %}

office-hours, browse 2가지 스킬만 주로 사용

<div><figure><img src="../../../../.gitbook/assets/image (155).png" alt=""><figcaption></figcaption></figure> <figure><img src="../../../../.gitbook/assets/image (156).png" alt=""><figcaption></figcaption></figure> <figure><img src="../../../../.gitbook/assets/image (133).png" alt=""><figcaption></figcaption></figure></div>

## 주 사용 스킬

### Office-hours

> 이 페이지에 설명된 **GStack의 Office-hours** 스킬은 YC(Y Combinator) 스타일의 파트너 역할을 하며, 제품을 직접 개발하거나 코드를 짜기 전에 **아이디어를 검증하고 기획을 정교하게 다듬어 디자인 문서(Design Doc)를 생성하는 스킬**입니다. 개발에 바로 착수하지 않고, "문제를 제대로 정의했는지"를 먼저 확인하는 데 초점을 맞춥니다. 이 스킬은 사용자의 목적에 따라 두 가지 모드로 작동합니다.
>
> ### 1. 스타트업 모드 (Startup Mode)
>
> 창업가나 기업 내 신사업 담당자를 위한 모드로, 아이디어의 현실성을 날카롭게 검증하는 \*\*6가지 강제 질문(The Six Forcing Questions)\*\*을 하나씩 던집니다.
>
> * **Q1. 수요의 현실 (Demand Reality):** 단순한 관심이나 대기열 등록이 아닌, 제품이 사라지면 진짜로 화를 낼 만한 실제 수요의 증거가 있는가?
> * **Q2. 현상 유지 (Status Quo):** 유저들이 지금은 이 문제를 어떻게 (불편하게라도) 해결하고 있으며, 그 우회 방식에 어떤 비용을 쓰고 있는가?
> * **Q3. 지독한 구체성 (Desperate Specificity):** 이 제품을 가장 필요로 하는 구체적인 가상/실제 인물(이름, 직책, 그 사람의 절박함)은 누구인가?
> * **Q4. 가장 좁은 교두보 (Narrowest Wedge):** 거대한 플랫폼을 만들기 전에, 이번 주에 당장 만들어서 돈을 받을 수 있는 가장 핵심적인 기능은 무엇인가?
> * **Q5. 관찰과 반전 (Observation & Surprise):** 유저가 제품을 쓰는 모습을 직접 관찰했을 때 상상을 벗어난 예상외의 행동이 있었는가?
> * **Q6. 미래 적합성 (Future-Fit):** 3년 뒤 세상이 바뀌었을 때 이 제품이 더 필수적이 될 것인가, 아니면 쓸모없어질 것인가?
>
> ### 2. 빌더 모드 (Builder Mode)
>
> 해커톤, 오픈소스, 학습, 재미를 위한 사이드 프로젝트를 하는 개발자를 위한 모드입니다. 압박 질문보다는 **아이디어를 확장하고 흥미를 극대화하는 브레인스토밍**을 진행합니다.
>
> * "이 아이디어의 가장 멋진(Coolest) 버전은 무엇일까?"
> * "사람들에게 보여줬을 때 '와!' 소리가 나오게 만들려면 무엇이 필요할까?"
>
> ### 💡 오피스 아워 스킬의 실행 예시
>
> #### 시나리오: "개발자를 위한 AI 작업 관리 도구" 아이디어가 있을 때
>
> 1. **스킬 호출:** 사용자가 "개발자용 AI 투두 앱 아이디어가 있는데 같이 생각 좀 해줘"라고 말하면 GStack이 자동으로 이 스킬을 실행합니다.
> 2. **컨텍스트 파악:** 기존 코드베이스의 CLAUDE.md나 기존 디자인 문서를 탐색해 관련 있는 설계가 있었는지 확인합니다.
> 3. **질문 진행 (스타트업 모드 예시):**
>
> * **GStack:** "현재 개발자들이 작업 관리를 위해 메모장이나 Jira를 쓰면서 매주 버리는 시간이 정확히 몇 시간인가요? 그 워크플로우를 구체적으로 말씀해주세요." (Q2 현상 유지 질문)
> * **사용자:** "보통 Jira 티켓 정리하고 오늘 할 일 메모장에 옮기느라 매일 30분씩 버려요."
>
> 4. **외부 의견 및 대안 제시:** 필요한 경우 다른 AI 모델(Codex 등)의 피드백을 받아 2\~3가지의 구현 접근 방식(가장 빠르게 배포할 수 있는 최소 기능 버전 vs 이상적인 아키텍처 버전)을 제안합니다.
> 5. **산출물 생성:** 대화가 끝나면 코드를 작성하는 대신, 구체적인 다음 행동 과제(Assignment)가 포함된 _**-design-**_**.md 형식의 기획/디자인 문서**를 생성하고 종료합니다. 이처럼 이 스킬은 무턱대고 코드부터 치기 전에 \*\*"이게 정말 만들 가치가 있는가?"\*\*를 치열하게 고민하게 도와주는 파트너 역할을 합니다.

### Browse

#### 정의

> #### 1. 브라우저 환경 제어
>
> * **세션 관리:** AI가 사용할 수 있는 전용 브라우저 세션을 시작하고 종료합니다.
> * **비주얼 확인:** 브라우저 창의 크기를 조절하거나 현재 화면을 스크린샷으로 캡처하여 AI가 시각적으로 페이지 상태를 확인할 수 있게 합니다.
>
> #### 2. 웹 페이지 탐색 및 상호작용
>
> * **URL 이동 및 새로고침:** 특정 웹사이트 주소로 이동하거나 페이지를 새로고침하고, 뒤로 가기/앞으로 가기 등의 내비게이션을 수행합니다.
> * **요소 조작:** 웹 페이지 내의 특정 버튼, 링크, 입력창을 찾아 \*\*클릭(Click)\*\*하거나 텍스트를 \*\*입력(Type)\*\*합니다.
> * **스크롤 기능:** 페이지를 위아래로 스크롤하여 숨겨진 콘텐츠를 로드하거나 확인할 수 있습니다.
>
> #### 3. 데이터 추출 및 분석
>
> * **콘텐츠 및 소스 가져오기:** 웹 페이지의 전체 텍스트 콘텐츠나 HTML 소스 코드를 추출합니다.
> * **요소 위치 파악:** AI가 화면의 어디를 조작해야 하는지 알 수 있도록 특정 웹 요소들의 위치 좌표 정보를 제공합니다.
>
> > 💡 **한 줄 요약**&#x20;
> >
> > AI가 사람처럼 웹사이트에 접속해 클릭하고, 타이핑하고, 화면을 보면서 정보를 수집하거나 웹 기반의 자동화 업무를 처리할 수 있게 만들어주는 스킬입니다.

#### Web Search 스킬과의 차이점

> #### 1. 작동 방식 (단순 조회 vs 직접 조작)
>
> * **기존 웹 검색:** AI가 검색 엔진 API를 통해 관련 문서나 웹페이지의 텍스트 데이터만 긁어와서(스크래핑) 읽습니다.
> * **Browse 스킬:** AI가 실제 **헤드리스 브라우저(크롬 등)를 실행**합니다. 웹페이지에 접속한 뒤 버튼을 클릭하고, 텍스트 상자에 글을 타이핑하고, 스크롤을 내리는 등 사람과 똑같이 화면과 상호작용합니다.
>
> #### 2. 접근 가능한 영역 (공개된 글 vs 로그인 및 인터랙션)
>
> * **기존 웹 검색:** 구글이나 네이버에 검색해서 나오는 '공개된 웹페이지'의 정보만 가져올 수 있습니다. 로그인 창이나 복잡한 입력 폼을 만나면 더 이상 진행하지 못합니다.
> * **Browse 스킬:** AI가 직접 아이디와 비밀번호를 입력해 **로그인**을 하거나, 드롭다운 메뉴를 선택하고, 달력에서 날짜를 고르는 등의 복잡한 프로세스를 수행할 수 있습니다.
>
> #### 3. 목적 (정보 요약 vs 업무 자동화)
>
> * **기존 웹 검색:** "오늘 날씨 어때?", "최근 뉴스 알려줘"처럼 단순히 **정보를 찾아내고 요약**하는 것이 목적입니다.
> * **Browse 스킬:** "OO 사이트에 로그인해서 이번 달 고지서 다운로드해 줘", "XX 쇼핑몰에서 가장 저렴한 상품 찾아서 장바구니에 담아줘"처럼 \*\*웹 기반의 실제 업무를 자동화(Agentic Workflow)\*\*하는 것이 목적입니다.
>
> > 💡 **한 줄 요약**
> >
> > 기존 검색은 웹의 내용을 \*\*'읽기(Read)'\*\*만 할 수 있다면, Browse 스킬은 웹사이트를 직접 \*\*'조작(Write/Action)'\*\*할 수 있는 능력을 AI에게 부여하는 것입니다.

#### 그럼 기존에 '로봇이 아닙니다' 등을 우회 가능한가?

> 결론부터 말씀드리면, **이론적으로는 가능하지만 실제로는 꽤 까다롭고 한계가 있는 영역**입니다. Browse 스킬의 메커니즘과 보안 시스템의 특성을 고려했을 때, 상황에 따라 다르게 작동합니다.
>
> #### 1. 단순한 체크박스 형태 (일부 가능)
>
> "나는 로봇이 아닙니다"라는 문구 옆의 네모 박스를 단순히 찾아 누르는 것은 기술적으로 가능합니다. Browse 스킬은 화면의 요소를 인식하고 클릭(Click)하는 기능이 있기 때문에, 해당 체크박스의 위치를 찾아 마우스 클릭 신호를 보낼 수 있습니다.
>
> #### 2. 이미지 맞추기 등 복잡한 캡차 (reCAPTCHA 등 - 어려움)
>
> 체크박스를 눌렀을 때 "버스를 모두 고르세요", "신호등이 포함된 타일을 선택하세요"와 같은 이미지 퍼즐이 뜨면 난이도가 급격히 올라갑니다.
>
> * **시각적 분석 필요:** AI가 캡처된 화면을 보고 어떤 그림이 버스인지 아주 정확하게 인식해야 합니다.
> * **우회 차단 시스템:** 구글의 reCAPTCHA 같은 최신 보안 시스템은 마우스가 움직이는 속도, 궤적, 클릭하는 타이밍 등을 분석해 사람이 아닌 '매크로(봇)'인지를 잡아냅니다. AI가 브라우저를 제어하는 방식은 이 보안망에 걸릴 확률이 매우 높습니다.
>
> #### 3. 실제 활용에서의 해결책
>
> 그래서 GStack의 Browse 스킬 같은 LLM 기반 에이전트 환경에서는 이 문제를 보통 두 가지 방식으로 우회합니다.
>
> * **인간 개입 (Human-in-the-loop):** AI가 웹서핑을 대행하다가 캡차 화면을 만나면 작업을 잠시 멈추고, "캡차가 나타났으니 사람이 직접 해결해 주세요"라고 사용자에게 요청합니다.
> * **우회 서비스 연동:** 캡차를 전문적으로 풀어주는 서드파티 서비스(2Captcha 등)의 API를 별도로 연동하여 해결하기도 합니다.
>
> > 💡 **한 줄 요약**
> >
> > 버튼을 누르는 시도는 할 수 있지만, 웹사이트의 보안 시스템이 AI의 자동 조작을 눈치채고 더 강력한 인증(이미지 맞추기 등)을 요구하기 때문에 100% 완벽하게 통과하기는 어렵습니다.

***

