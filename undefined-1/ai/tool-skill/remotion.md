# Remotion

{% embed url="https://www.remotion.dev/docs/ai/skills" %}

## 개요

> Remotion = React로 프로그래매틱 비디오 만드는 프레임워크.
>
> &#x20; 핵심 개념:
>
> &#x20; \- HTML/CSS/JS로 비디오 프레임 그림
>
> &#x20; \- useCurrentFrame() hook으로 현재 프레임 번호 받아 애니메이션
>
> &#x20; \- 렌더링 완료되면 MP4/GIF/WebM 출력
>
> <br>
>
> &#x20; 쓰이는 곳:
>
> &#x20; \- 코드로 자동 생성되는 유튜브/SNS 영상
>
> &#x20; \- 데이터 시각화 영상 (매일 달라지는 차트 등)
>
> &#x20; \- 프로그래매틱 광고 소재 대량 생성
>
> &#x20; \- GitHub Unwrapped 같은 개인화 연말 리포트 영상
>
> <br>
>
> &#x20; 예시:
>
> &#x20; const MyVideo = () => {
>
> &#x20;   const frame = useCurrentFrame(); // 0, 1, 2, 3...
>
> &#x20;   return \<div style=\{{ opacity: frame / 30 \}}>Hello\</div>;
>
> &#x20; };
>
> &#x20; → 30프레임에 걸쳐 fade-in하는 비디오
>
> &#x20; 한마디로: "영상판 React". 디자인 툴 대신 코드로 영상 만들 때 씀.

주로 영상 자동화에 가깝다.

영상을 분석하진 못하고, 단순 합성 & 편집 형태만 가능

## 설치법

{% code overflow="wrap" %}
```bash
npx skills add remotion-dev/skills
```
{% endcode %}

## 새로운 프로젝트 생성

{% code overflow="wrap" %}
```bash
bun create video
```
{% endcode %}

