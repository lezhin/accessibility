# 레진 웹 접근성 가이드라인
모두를 위한 설계. 레진 웹 접근성 가이드라인.

1. [의미를 전달하고 있는 이미지에 대체 텍스트를 제공한다.](#alt)
2. [전경 콘텐츠와 배경은 4.5:1 이상의 명도 대비를 유지한다.](#contrast)
3. [화면을 400%까지 확대할 수 있다.](#zoom)
4. [키보드만으로 조작할 수 있다.](#keyboard)
5. [사용할 수 있는 충분한 시간을 제공한다.](#time)
6. [발작을 유발하는 콘텐츠를 제공하지 않는다.](#seizure)
7. [반복되는 콘텐츠 블록을 건너뛸 수 있다.](#bypass)
8. [모든 문서의 제목은 고유하고 식별할 수 있다.](#title)
9. [링크와 버튼 텍스트는 콘텐츠의 목적을 알 수 있다.](#link)
10. [섹션에는 의미 있는 마크업과 헤딩이 있다.](#outline)
11. [문서의 휴먼 랭귀지 속성을 제공한다.](#lang)
12. [문맥 변경은 예측할 수 있다.](#predict)
13. [폼 콘트롤 요소에 설명을 제공한다.](#form)
14. [실수를 예방하고 정정하는 것을 돕는다.](#assist)
15. [HTML 문법을 준수한다.](#html)

보편적인 웹 서비스를 제공함으로써 "**모두를 즐겁게 하라**"는 우리의 모토를 실현하고자 합니다. 레진엔터테인먼트에서 제공하는 모든 웹 서비스는 '**레진 웹 접근성 가이드라인**'을 준수해야 합니다. 데스크톱, 태블릿, 모바일, 하이브리드 앱에 이르기까지 웹 기술을 통해 구현하는 모든 서비스가 이 가이드라인의 적용 대상입니다.

이 가이드라인은 [WCAG 2.1](https://www.w3.org/TR/WCAG21/)이 근간이며 가이드라인에서 설명하지 않거나 애매한 주제는 WCAG 2.1의 수준 A 항목과 AA 항목의 지침 및 평가 방법을 따라야 합니다. 레진 웹 접근성 가이드라인은 레진 고유의 콘텐츠에 대응하는 WCAG 2.1 가이드라인에 대한 이해를 돕고 손쉽게 평가할 수 있도록 소개한 것으로써 고객에게 웹 서비스를 제공하기 전 준수해야 할 최소한의 요구사항입니다.

이 가이드라인은 웹 기술(HTML, CSS, JavaScript)에 대한 사전 지식을 요구합니다.

---

## 1. 의미를 전달하고 있는 이미지에 대체 텍스트를 제공한다. <a id="alt" href="#alt">#</a>
* 대체 텍스트는 이미지의 시각적 의도와 동등한 내용을 전달한다.
* 대체 텍스트는 중복으로 제공하지 않는다.

` `

    <!-- X -->
    <img src="lezhin.png">
    <img src="lezhin.png" alt>
    <img src="lezhin.png" alt="">
    <img src="lezhin.png" title="레진엔터테인먼트">
    <img src="lezhin.png" alt="레진엔터테인먼트" title="레진엔터테인먼트">

    <!-- O -->
    <img src="lezhin.png" alt="레진엔터테인먼트">

    <!-- X -->
    <a href="/">
        <img src="lezhin.png" alt="레진엔터테인먼트"> 레진엔터테인먼트
    </a>

    <!-- O -->
    <a href="/">
        <img src="lezhin.png" alt> 레진엔터테인먼트
    </a>

    <!-- X -->
    <a href="/" style="background:url(lezhin.png) no-repeat"></a>

    <!-- O -->
    <a href="/" style="background:url(lezhin.png) no-repeat">레진엔터테인먼트</a>

### 기대 효과
* 전맹 사용자에게 음성 해설을 제공할 수 있다.

### 관련 표준
* [1.1.1 Non-text Content](https://www.w3.org/TR/WCAG21/#non-text-content)

### 평가 도구
* [OpenWAX](https://chrome.google.com/webstore/detail/openwax/bfahpbmaknaeohgdklfbobogpdngngoe?hl=ko)

---

## 2. 전경 콘텐츠와 배경은 4.5:1 이상의 명도 대비를 유지한다. <a id="contrast" href="#contrast">#</a>
* 전경 콘텐츠는 정보를 전달하고 있는 '문자, 아이콘, 콘트롤(a, button, input, select, textarea)'의 선과 면을 의미한다.
* 문자 크기가 bold 19px 이상 또는 normal 24px 이상인 경우 3:1 이상의 명도 대비를 유지한다.
* 아이콘, 콘트롤 등 시각 정보가 3px 이상 두꺼운 경우 3:1 이상의 명도 대비를 유지한다.

` `

    <!-- X -->
    <body style="background:#fff">
        <p style="color:#777">레진엔터테인먼트</p>
    </body>

    <!-- O -->
    <body style="background:#fff">
        <p style="color:#767676">레진엔터테인먼트</p>
    </body>

    <!-- X -->
    <body style="background:#fff">
        <input style="border:1px solid #777">
    </body>

    <!-- O -->
    <body style="background:#fff">
        <input style="border:1px solid #767676">
    </body>

### 기대 효과
* 저시력 사용자가 내용을 빠르게 인지할 수 있다.

### 관련 표준
* [1.4.3 Contrast(Minimum)](https://www.w3.org/TR/WCAG21/#contrast-minimum)
* [1.4.11 Graphics Contrast](https://www.w3.org/TR/WCAG21/#graphics-contrast)
* [1.4.12 User Interface Component Contrast(Minimum)](https://www.w3.org/TR/WCAG21/#user-interface-component-contrast-minimum)

### 평가 도구
* [Colour Contrast Check](https://snook.ca/technical/colour_contrast/colour.html#fg=33FF33,bg=333333)
* [ColorA11y](https://chrome.google.com/webstore/detail/colora11y/icfneoldcbdmgaiocnnobpbbjncdfbfb?hl=ko)

---

## 3. 화면을 400%까지 확대할 수 있다. <a id="zoom" href="#zoom">#</a>
* 너비 1,280 픽셀 해상도 모니터에서 400%까지 확대할 수 있다. 모바일 단말에서는 테스트하지 않는다.
* 화면을 400% 확대한 상태에서 내용과 기능에 손실이 없어야 하고, 2차원 스크롤이 발생하지 않아야 한다.

` `

    <!-- X -->
    http://www.president.go.kr/

    <!-- O -->
    https://www.whitehouse.gov/

### 기대 효과
* 저시력 사용자가 내용을 빠르게 인지할 수 있다.
* 하나의 소스 만으로 모든 해상도의 출력 장치에 대응 가능하다.

### 관련 표준
* [1.4.10 Zoom content](https://www.w3.org/TR/WCAG21/#zoom-content)

---

## 4. 키보드만으로 조작할 수 있다. <a id="keyboard" href="#keyboard">#</a>
* 구현된 키보드 접근 순서는 논리적으로 설명할 수 있어야 한다.
* 초점을 받은 요소는 시각적 단서를 제공해야 한다.

` `

    <!-- X -->
    a:hover{ color: #000; }

    <!-- O -->
    a:hover,
    a:focus{ color: #000; }

    <!-- X -->
    $(document).on("mouseover", ".gnb a", function() { ... });

    <!-- O -->
    $(document).on("mouseover focus", ".gnb a", function() { ... });

### 기대 효과
* 전맹 또는 상지 장애가 있는 사용자와 키보드를 선호하는 사용자의 탐색과 조작을 돕는다.

### 관련 표준
* [2.1.1 Keyboard](https://www.w3.org/TR/WCAG21/#keyboard)
* [2.1.2 No Keyboard Trap](https://www.w3.org/TR/WCAG21/#no-keyboard-trap)
* [2.4.3 Focus Order](https://www.w3.org/TR/WCAG21/#focus-order)
* [2.4.7 Focus Visible](https://www.w3.org/TR/WCAG21/#focus-visible)

---

## 5. 사용할 수 있는 충분한 시간을 제공한다. <a id="time" href="#time">#</a>
* 시간 제한이 있는 정보는 시간 제한을 끄거나, 또는 최소 20초 이상 10회까지 연장할 수 있다.
* 자동으로 갱신되는 정보에는 '정지, 이전, 다음' 기능을 제공한다.

` `

    <!-- X -->
    10초 후 다음 페이지로 넘어갑니다. [다음 페이지로 즉시 이동]

    <!-- O -->
    20초 후 다음 페이지로 넘어갑니다. [취소] [다음 페이지로 즉시 이동]
    20초 후 다음 페이지로 넘어갑니다. [20초 연장] [다음 페이지로 즉시 이동]

    <!-- X -->
    콘텐츠가 자동으로 슬라이드 되고 있는 상황에서 정지하거나 이전, 다음 콘텐츠를 탐색할 수 없다.

    <!-- O -->
    콘텐츠가 자동으로 슬라이드 되고 있지만 정지, 이전, 다음 기능을 제공하고 있다.

### 기대 효과
* 학습장애 또는 난독증세가 있는 사람이 내용을 이해할 수 있다.

### 관련 표준
* [2.2.1 Timing Adjustable](https://www.w3.org/TR/WCAG21/#timing-adjustable)
* [2.2.2 Pause, Stop, Hide](https://www.w3.org/TR/WCAG21/#pause-stop-hide)

---

## 6. 발작을 유발하는 콘텐츠를 제공하지 않는다. <a id="seizure" href="#seizure">#</a>
* 1초에 3~50회 사이의 번쩍이는 콘텐츠는 광과민성 발작을 유발할 수 있다.
* 광과민성 발작은 소아 또는 간질 경험이 있는 사람에게 더 위험하다.

` `

    포켓몬 발작 사고 영상 - https://www.youtube.com/watch?v=gwoQRKCEHgY // 소아 또는 간질 경험이 있는 사람에게 발작 위험.

### 기대 효과
* 소아 또는 간질 경험이 있는 사람의 발작을 예방할 수 있다.
### 관련 표준
* [2.3.1 Three Flashes or Below Threshold](https://www.w3.org/TR/WCAG21/#three-flashes-or-below-threshold)
* [2.3.2 Three Flashes](https://www.w3.org/TR/WCAG21/#three-flashes)

---

## 7. 반복되는 콘텐츠 블록을 건너뛸 수 있다. <a id="bypass" href="#bypass">#</a>
* 일반적으로 글로벌 탐색 바와 로컬 탐색 바는 반복되는 콘텐츠 블록이다.
* 반복되는 콘텐츠 블록이 있는 경우 페이지 시작 위치에 '본문으로 건너뛰기' 링크를 제공한다.

` `

    <!-- X -->
    <body>
        <h1>레진엔터테인먼트</h1>
        <nav>...</nav>
        <main>...</main>

    <!-- O -->
    <body>
        <a href="#main">본문으로 건너뛰기</a>
        <h1>레진엔터테인먼트</h1>
        <nav>...</nav>
        <main id="main">...</main>

### 기대 효과
* 전맹 또는 상지 장애가 있는 사용자와 키보드를 선호하는 사용자의 탐색과 조작을 돕는다.

### 관련 표준
* [2.4.1 Bypass Blocks](https://www.w3.org/TR/WCAG21/#bypass-blocks)

---

## 8. 모든 문서의 제목은 고유하고 식별할 수 있다. <a id="title" href="#title">#</a>
* 제목 콘텐츠를 문서마다 다르게 설명함으로써 현재 문서의 용도를 식별할 수 있다.

` `

    <!-- X -->
    <head>
        <title>레진코믹스<title>

    <!-- O -->
    <head>
        <title>준법시민(99회) - 레바툰 - 레진코믹스<title>

### 기대 효과
* 전맹 사용자가 링크 이동 결과를 음성으로 확인할 수 있다.
* 문서의 용도를 빠르게 파악할 수 있다.
* 검색엔진이 올바른 페이지를 수집하도록 돕는다.
* 유저 에이전트 탭의 식별 가능성이 높아진다.

### 관련 표준
* [2.4.2 Page Titled](https://www.w3.org/TR/WCAG21/#page-titled)

---

## 9. 링크와 버튼 텍스트는 콘텐츠의 목적을 알 수 있다. <a id="link" href="#link">#</a>
* 주변 콘텐츠와 분리하여 독립적으로 접근해도 링크 또는 버튼의 목적을 알 수 있어야 한다.
* 링크 또는 버튼에 독립적으로 접근하여 이해하기 어려운 경우 동일한 단락, 목록, 셀, 연결된 헤더셀(p, li, td, th)에 링크 또는 버튼의 목적을 설명해야 한다.

` `

    <!-- X -->
    <a href="#" download>설치하기</a>
    <button type="button">삭제하기</button>

    <!-- O -->
    <a href="#" download>레진코믹스 안드로이드 애플리케이션 설치하기</a>
    <p>레진코믹스 안드로이드 애플리케이션 <a href="#" download>설치하기</a></p>
    <li>레진코믹스 안드로이드 애플리케이션 <a href="#" download>설치하기</a></li>
    <td>레진코믹스 안드로이드 애플리케이션 <a href="#" download>설치하기</a></td>
    <tr>
        <th scope="row">레진코믹스 안드로이드 애플리케이션</th>
        <td><a href="#" download>설치하기</a></td>
    </tr>

    <!-- O -->
    <button type="button">구매내역 삭제하기</button>
    <p>구매내역 <button type="button">삭제하기</button></p>
    <li>구매내역 <button type="button">삭제하기</button></li>
    <td>구매내역 <button type="button">삭제하기</button></td>
    <tr>
        <th scope="row">구매내역</th>
        <td><button type="button">삭제하기</button></td>
    </tr>

### 기대 효과
* 전맹 사용자가 링크에 독립적으로 또는 순차적으로 접근하는 경우 링크의 목적을 음성으로 전달할 수 있다.

### 관련 표준
* [2.4.4 Link Purpose(In Context)](https://www.w3.org/TR/WCAG21/#link-purpose-in-context)

### 평가 도구
* [OpenWAX](https://chrome.google.com/webstore/detail/openwax/bfahpbmaknaeohgdklfbobogpdngngoe?hl=ko)

---

## 10. 섹션에는 의미 있는 마크업과 헤딩이 있다. <a id="outline" href="#outline">#</a>
* 섹션 콘텐츠는 의미에 알맞은 article, section, nav, aside 요소로 마크업한다.
* 섹션 콘텐츠에는 문서의 개요 체계에 알맞은 헤딩(h1~h6)을 제공한다.
* 명시적 헤딩 기법을 사용한다. 명시적 헤딩 기법은 하나의 문서에 h1 요소를 한 번 사용한다.

` `

    <!-- X -->
    <div class="article">...</div>
    <div class="section">...</div>
    <div class="nav">...</div>
    <div class="aside">...</div>

    <!-- O -->
    <article>
        <h2>...</h2>
        ...
    </article>
    <section>
        <h2>...</h2>
        ...
    </section>
    <nav>
        <h2>...</h2>
        ...
    </nav>
    <aside>
        <h2>...</h2>
        ...
    </aside>

### 기대 효과
* 보조기기 사용자가 원하는 탐색 지점으로 빠르게 건너 뛸 수 있다.
* 검색엔진이 올바를 페이지를 수집하도록 돕는다.
* 유저 에이전트 확장 기능 사용자에게 문서 개요를 전달할 수 있다.

### 관련 표준
* [2.4.6 Headings and Labels](https://www.w3.org/TR/WCAG21/#headings-and-labels)
* [2.4.10 Section Headings](https://www.w3.org/TR/WCAG21/#section-headings)

### 평가 도구
* [HTML5 Outliner](https://chrome.google.com/webstore/detail/html5-outliner/afoibpobokebhgfnknfndkgemglggomo)

---

## 11. 문서의 휴먼 랭귀지 속성을 제공한다. <a id="lang" href="#lang">#</a>
* html 요소에 lang 속성을 제공한다.
* 한글, 영문, 일문, 중문에는 이를 식별하기 위한 [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) 코드값 ko, en, ja, zh가 있다.

` `

    <!-- X -->
    <html>

    <!-- O -->
    <html lang="ko">

### 기대 효과
* 보조기기와 검색엔진이 문서의 휴먼 랭귀지를 식별할 수 있다.

### 관련 표준
* [3.1.1 Language of Page](https://www.w3.org/TR/WCAG21/#language-of-page)
* [3.1.2 Language of Parts](https://www.w3.org/TR/WCAG21/#language-of-parts)

### 평가 도구
* [OpenWAX](https://chrome.google.com/webstore/detail/openwax/bfahpbmaknaeohgdklfbobogpdngngoe?hl=ko)

---

## 12. 문맥 변경은 예측할 수 있다. <a id="predict" href="#predict">#</a>
* 사용자가 실행하기 전까지는 문서를 갱신(이동, 추가, 삭제, 재배치)하거나, 팝업(새 창, 레이어)을 띄우거나, 초점을 다른 곳으로 옮기지 않는다.
* 사용자가 초점을 넣거나 마우스를 올리는 것은 기능을 실행하기 위한 의도로 보지 않기 때문에 문맥을 변경하면 안 된다.
* '대한민국' 선택의 결과로 대한민국의 '시/군/구'를 선택하는 항목이 등장했다면 이것은 문맥의 변화가 아니다.

` `

    <!-- X -->
    초점을 넣었을 뿐인데 자동으로 페이지 갱신 또는 이동.
    페이지 로드 시 자동 팝업.
    초점 자동 이동.

    <!-- O -->
    클릭 또는 리턴(엔터) 키를 통해 페이지 갱신 또는 이동.
    클릭 또는 리턴(엔터) 키를 통해 팝업 생성.
    초점을 자동으로 옮기지 않음.

### 기대 효과
* 보조 기기 사용자가 혼란에 빠지는 것을 예방할 수 있다.

### 관련 표준
* [3.2.1 On Focus](https://www.w3.org/TR/WCAG21/#on-focus)
* [3.2.2 On Input](https://www.w3.org/TR/WCAG21/#on-input)
* [3.2.5 Change on Request](https://www.w3.org/TR/WCAG21/#change-on-request)

---

## 13. 폼 콘트롤 요소에 설명을 제공한다. <a id="form" href="#form">#</a>
* 모든 input, textarea, select 요소에는 콘트롤을 설명하는 label 요소를 맵핑하거나 또는 title 속성을 제공한다.

` `

    <!-- X -->
    <form>
        <input type="search">
        <button>검색</button>
    </form>

    <!-- O -->
    <form>
        <label for="search">검색</label>
        <input id="search" type="search">
        <button>검색</button>
    </form>

    <!-- O -->
    <form>
        <input type="search" title="검색">
        <button>검색</button>
    </form>

### 기대 효과
* 보조기기가 폼 콘트롤에 독립적으로 접근했을 때 콘트롤에 대한 설명을 제공할 수 있다.

### 관련 표준
* [2.4.6 Headings and Labels](https://www.w3.org/TR/WCAG21/#headings-and-labels)
* [3.3.2 Labels or Instructions](https://www.w3.org/TR/WCAG21/#labels-or-instructions)

### 평가 도구
* [OpenWAX](https://chrome.google.com/webstore/detail/openwax/bfahpbmaknaeohgdklfbobogpdngngoe?hl=ko)

---

## 14. 실수를 예방하고 정정하는 것을 돕는다. <a id="assist" href="#assist">#</a>
* 입력 오류를 자동으로 감지할 수 있는 경우에만 이 지침을 적용한다. 예를 들면 이름을 잘못 입력하는 경우 정정 의견을 제시할 수 없다.
* 오류 항목이 무엇인지 식별할 수 있도록 문자로 알리고 정정 의견을 제시한다. 예를 들면 "생년월일 양식에 오류가 있습니다. 입력 형식은 yyyy-mm-dd 입니다."
* 정정 의견은 보안을 유지하는 수준에서 제시한다. 예를 들면 "아이디 또는 비밀번호 입력 오류."
* 입력 내용을 전송하기 전 검토 후 교정할 수 있다. 또는 제출한 내용을 되돌릴 수 있다.

` `

    <!-- X -->
    오류 입력 양식에 붉은 색 보더 처리. // 시각에 의존하고 있다. 문자로 알려야 한다.
    "입력 양식에 오류가 있습니다." // 오류 식별 불가.
    "로그인 오류. 비밀번호는 특수문자, 숫자, 알파벳을 하나 이상 포함해야 합니다." // 정정 의견이 보안을 해치고 있음.
    여러 단계(여러 페이지)에 걸쳐 작성한 내용 중 이전 단계의 내용을 검토할 수 없고 제출 후 수정할 수 없음. // 제출 전 또는 제출 수 수정할 수 있어야 한다.

    <!-- O -->
    "생년월일 양식에 오류가 있습니다. 입력 형식은 yyyy-mm-dd 입니다." // 오류 식별 가능. 정정 의견 제시.
    "아이디 또는 비밀번호 입력 오류. 5회 이상 오류 발생 시 계정잠금 상태로 전환합니다." // 오류 식별 가능. 정정 의견 제시. 보안을 해치지 않음.
    여러 단계(여러 페이지)에 걸쳐 작성한 내용 중 이전 단계의 내용을 검토 후 수정할 수 있음. 또는 이전 단계의 내용을 수정할 수 없지만 제출 후 수정할 수 있음.

### 기대 효과
* 사용자가 실수하지 않도록 예방하고 실수를 교정할 수 있다.

### 관련 표준
* [3.3.1 Error Identification](https://www.w3.org/TR/WCAG21/#error-identification)
* [3.3.3 Error Suggestion](https://www.w3.org/TR/WCAG21/#error-suggestion)
* [3.3.4 Error Prevention (Legal, Financial, Data)](https://www.w3.org/TR/WCAG21/#error-prevention-legal-financial-data)
* [3.3.6 Error Prevention (All)](https://www.w3.org/TR/WCAG21/#error-prevention-all)

---

## 15. HTML 문법을 준수한다. <a id="html" href="#html">#</a>
* 시작 태그에서 닫는(self-closing) 요소를 제외하고 시작 태그, 종료 태그, 따옴표를 생략하지 않는다.
* 명세에 따라 중첩한다.
* 속성을 중복 선언하지 않는다.
* 모든 id 속성의 값은 하나의 문서 안에서 중복 없이 유일하다.

` `

    <!-- X -->
    <div><span>...</div> // span 종료 태그 생략 오류.
    <span><a><div>...</div></a></span> // span 요소가 div를 감싼 것은 오류.
    <div class="aaa" class="bbb">...</div> // 속성은 한 번만 선언해야 한다.
    <div id="xyz">...</div><div id="xyz">...</div> // xyz 값은 페이지에서 유일해야 한다.

    <!-- O -->
    <div><span>...</span></div>
    <div><a><div>...</div></a></div>
    <div class="aaa bbb">...</div>
    <div id="abc">...</div><div id="xyz">...</div>

### 기대 효과
* 보조기기의 웹 문서 해석 오류를 예방할 수 있다.

### 관련 표준
* [4.1.1 Parsing](https://www.w3.org/TR/WCAG21/#parsing)

### 평가 도구
* [W3C Markup Validation Service](https://validator.w3.org/)

---

## 관련 표준
* [WCAG 2.1](https://www.w3.org/TR/WCAG21/)(WD)
* [HTML 5.1](https://www.w3.org/TR/html51/)(R)
* [WAI-ARIA 1.1](https://www.w3.org/TR/wai-aria-1.1/)(CR)

## License
Under MIT License. Copyright &copy; 2017 @lezhin.



