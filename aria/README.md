# 레진 WAI-ARIA 가이드라인

[WAI-ARIA](https://www.w3.org/TR/wai-aria-1.1/)는 HTML의 접근성 문제를 보완하는 W3C 명세입니다. WAI-ARIA는 HTML 요소에 `role` 또는 `aria-*` 속성을 추가하여 콘텐츠의 '역할(roles), 상태(states), 속성(properties)' 정보를 보조기기에 제공합니다.



1. [HTML을 의미있게 작성한다.](#html)
2. [탭 목록, 탭, 탭 패널(`role="tablist|tab|tabpanel"`).](#tab)
3. [툴팁(`role="tooltip"`).](#tooltip)
4. [알럿(`role="alert"`).](#alert)
5. [알럿 대화상자(`role="alertdialog"`).](#alertdialog)
6. [대화상자(`role="dialog"`).](#dialog)
7. [탐색(`nav`, `role="navigation"`).](#nav)
8. [보충(`aside`, `role="complementary"`).](#aside)
9. [의미 없음(`role="none"`).](#none)
10. [현재 항목(`aria-current="token"`).](#aria-current)
11. [선택 항목(`aria-selected="true|false|undefined"`).](#aria-selected)
12. [팝업 있음(`aria-haspopup="token"`)](#aria-haspopup)
13. [확장(`aria-expanded="true|false|undefined"`)](#aria-expanded)
14. [누름(`aria-pressed="tristate"`)](#aria-pressed)
15. [제어 대상(`aria-controls="ID reference list"`)](#aria-controls)
16. [실시간(`aria-live="token"`)](#aria-live)
17. [설명 참조(`aria-labelledby="ID reference list"`)](#aria-labelledby)
18. [설명(`aria-label="string"`)](#aria-label)
19. [자세한 설명 참조(`aria-describedby="ID reference list"`)](#aria-describedby)
99. [참고 문서](#references)



```html
<!-- 레진엔터테인먼트에서 사용하고 있는 WAI-ARIA -->

<!-- 역할(roles) -->
<element role="tablist">
<element role="tab">
<element role="tabpanel">
<element role="tooltip">
<element role="alert">
<element role="alertdialog">
<element role="dialog">
<element role="navigation">
<element role="complementary">
<element role="none">

<!-- 상태(states) -->
<element aria-current="page|step|location|date|time|true|false(default)">
<element aria-selected="false|true|undefined(default)">
<element aria-haspopup="true|menu|dialog|listbox|tree|grid|false(default)">
<element aria-expanded="true|false|undefined(default)">
<element aria-pressed="true|false|mixed|undefined(default)">

<!-- 속성(properties) -->
<element aria-controls="ID reference list">
<element aria-live="polite|assertive|off(default)">
<element aria-labelledby="ID reference list">
<element aria-label="string">
<element aria-describedby="ID reference list">
```



---



## 1. HTML을 의미있게 작성한다. <a id="html" href="#html">#</a>
대부분의 WAI-ARIA 명세는 HTML 요소와 속성을 흉내내는 것입니다. 올바른 HTML을 사용한다면 WAI-ARIA 사용을 최소화할 수 있습니다. WAI-ARIA를 사용하기에 앞서 HTML을 의미있게 사용했는지 충분히 검토합니다.

```html
<!-- X -->
<a href="#" role="button">

<!-- O -->
<button type="button">
```
보조기기는 두 가지 예제를 모두 '버튼'으로 간주할 것입니다. 그러나 첫 번째 예제의 경우 브라우저는 문맥 메뉴를 통해 링크와 관련된 기능(새 탭에서 링크 열기, 링크 주소 복사 등)을 제공하게 되고 사용자를 혼란스럽게 합니다. 또한 첫 번째 예제에서 '버튼' 이라는 설명을 들은 보조기기 사용자는 '스페이스'키를 눌러 버튼 기능을 사용하려고 시도할 수 있습니다. 하지만 `a` 요소는 '엔터' 키 만으로 실행할 수 있습니다. `button` 요소는 '엔터' 키와 '스페이스' 키로 실행할 수 있기 때문에 `a` 요소로부터 '버튼' 이라는 설명을 전해들은 보조기기 사용자를 혼란스럽게 합니다. 결국 올바른 HTML의 선택은 사용자 경험과 접근성 측면에서 모두 중요합니다.



---



## 2. 탭 목록, 탭, 탭 패널(`role="tablist|tab|tabpanel"`). <a id="tab" href="#tab">#</a>

탭은 스타일을 의미하는 것이 아니라 현재 페이지 내용에 색인을 제공하는 구조(tablist, tab, tabpanel)를 의미합니다. 사이트 탐색 도구에 해당하는 요소는 `nav > h2 + ul` 또는 `aside > h2 + ul` 구조로 마크업 합니다.

```html
<!-- O: 앵커 형식 탭 -->
<div class="weekly">
    <div role="tablist">
        <a id="mon-anchor" href="#mon" role="tab" aria-selected="true">월</a>
        <a id="tue-anchor" href="#tue" role="tab" aria-selected="false">화</a>
    </div>
    <div id="mon" tabindex="0" role="tabpanel" aria-labelledby="mon-anchor">
        월요일엔 빨간 장미를...
    </div>
    <div id="tue" tabindex="0" role="tabpanel" aria-labelledby="tue-anchor" hidden>
        화요일엔 노란 장미를...
    </div>
</div>

<!-- O: 버튼 형식 탭 -->
<div class="weekly">
    <div role="tablist">
        <button type="button" id="mon-anchor" aria-controls="mon" role="tab" aria-selected="true">월</button>
        <button type="button" id="tue-anchor" aria-controls="tue" role="tab" aria-selected="false">화</button>
    </div>
    <div id="mon" tabindex="0" role="tabpanel" aria-labelledby="mon-anchor">
        월요일엔 빨간 장미를...
    </div>
    <div id="tue" tabindex="0" role="tabpanel" aria-labelledby="tue-anchor" hidden>
        화요일엔 노란 장미를...
    </div>
</div>
```

`role` 속성은 값에 따라 적용할 수 있는 HTML 요소가 제한되어 있습니다. 예를 들면 `role="tabpanel"` 속성은 `<ul>`요소에 사용할 수 없으므로 적용 시 HTML5 요소 명세를 확인해야 합니다.



---



## 3. 툴팁(`role="tooltip"`). <a id="tooltip" href="#tooltip">#</a>

툴팁은 앵커 또는 폼 콘트롤 요소에 대한 참고용 콘텐츠입니다. 보통 마우스 오버 또는 키보드 초점을 받으면 표시하는 내용이지만 화면에 항상 표시할 수도 있습니다. 툴팁 요소에 `role="tooltip"` 속성으로 명시할 수 있습니다. 툴팁을 유발하는 앵커 또는 콘트롤에 `aria-describedby="ID reference list"` 속성을 명시하여 연결합니다.

```html
<!-- O: 인풋 툴팁 -->
<label for="tel">전화번호</label>
<input id="tel" type="tel" aria-describedby="TIP-TEL">
<p id="TIP-TEL" role="tooltip" hidden>하이픈(-) 없이 숫자만 입력.</p>

<!-- O: 버튼 툴팁 -->
<button aria-describedby="TIP-DEL">삭제</button>
<p id="TIP-DEL" role="tooltip" hidden>삭제 후 복원할 수 없음.</p>
```

`role="alert"` 또는 `role="alertdialog"` 또는 `role="dialog"` 콘텐츠와 혼동하지 않도록 유의합니다.



---



## 4. 알럿(`role="alert"`). <a id="alert" href="#alert">#</a>

알럿은 일시적으로 민감한 정보를 사용자에게 전달하는 콘텐츠입니다. 운영체제 또는 브라우저에서 제공하는 시스템 알럿 대신 HTML 마크업으로 스타일 처리한 알럿을 제공할 수 있습니다.

초점을 받을 필요가 없는 알럿은 `role="alert"` 으로 처리합니다. 알럿 발생 시 보조기기에 실시간으로 알림을 전달하려면 `aria-live="assertive"` 속성을 명시합니다.

```html
<!-- O: 알럿 -->
<div role="alert" aria-live="assertive">
    <p>로그인 후 이용할 수 있습니다.</p>
</div>
```

초점을 받을 수 있는 사용자 인터렉션 요소를 포함하고 있다면 알럿 대화상자 `role="alertdialog"` 또는 대화상자 `role="dialog"`를 사용합니다.

사용자 입력 콘트롤(`input`, `textaria`)의 실시간 오류를 표시하는 경우라면 알럿 대신 콘트롤 요소에 `aria-invalid="true|false"` 속성과 `aria-errormessage="ID reference"` 속성을 사용합니다.



---



## 5. 알럿 대화상자(`role="alertdialog"`). <a id="alertdialog" href="#alertdialog">#</a>

사용자 동의 또는 확인이 필요한 인터렉션 요소(`input`, `button`)를 포함한 상태로 다른 과업을 차단하는 경우 알럿 대화상자 `role="alertdialog"`를 사용합니다. 사용자 입력 없이 '확인, 취소' 버튼을 제공하는 경우에 적절합니다. 알럿 대화상자 발생 시 보조기기에 실시간으로 알림을 전달하려면 `aria-live="assertive"` 속성을 명시합니다.

 알럿 대화상자에는 `aria-labelledby="ID reference list"` 그리고 `aria-describedby="ID reference list"` 속성으로 알럿 대화상자의 제목과 설명을 연결합니다.

 알럿 대화상자는 다른 과업을 차단해야 하기 때문에 모달 윈도우 스타일로 처리한 다음 `aria-modal="true"` 속성을 추가합니다.

 알럿 대화상자를 표시할 때 키보드 초점을 대화상자 내부 첫 번째 콘트롤(예를 들면 '확인' 버튼 또는 '인풋')으로 옮겨야 합니다. 알럿 대화상자를 표시하는 동안 초점은 대화상자 안에서 벗어나지 않아야 합니다.

```html
<!-- O: 알럿 대화상자 -->
<div role="alertdialog" aria-live="assertive" aria-modal="true" aria-labelledby="TITLE" aria-describedby="DESCRIPTION">
    <h2 id="TITLE">레진패스 안내</h2>
    <p id="DESCRIPTION">이 작품의 유료 에피소드 열람 시 자동으로 구매합니다. 레진패스를 적용하시겠습니까?</p>
    <button type="button">레진패스 적용</button>
    <button type="button">취소</button>
</div>
```

사용자가 응답할 필요 없는 내용이라면 `role="alert"` 속성이 적절합니다. 사용자가 하위창 맥락으로 벗어나 정보를 입력(`input`, `textarea`, `select`, `button`)하는 경우라면 대화상자 `role="dialog"`가 적절합니다.



---



## 6. 대화상자(`role="dialog"`). <a id="dialog" href="#dialog">#</a>

대화상자 `role="dialog"`는 사용자 인터렉션이 필요한 현재 문서의 하위창(마치 윈도우 팝업)입니다. 사용자가 정보를 입력하거나 응답하도록 하는 내용(`input`, `textarea`, `select`, `button`)을 반드시 포함합니다.

대화상자에는 `aria-labelledby="ID reference list"` 또는 `aria-label="string"` 속성으로 설명을 제공합니다.

대화상자를 표시할 때 키보드 초점을 대화상자 내부 첫 번째 콘트롤으로 옮겨야 합니다. 대화상자를 표시하는 동안 초점은 대화상자 안에서 벗어나지 않아야 합니다.

모달 윈도우 스타일로 표시할 것인지 여부는 선택 사항입니다. 모달 윈도우 스타일로 처리하는 경우 `aria-modal="true"` 속성을 추가합니다.

```html
<!-- O: 대화상자 -->
<form role="dialog" aria-live="polite" aria-modal="true" aria-labelledby="TITLE">
    <h2 id="TITLE">로그인</h2>
    <label for="ID">아이디</label>
    <input id="ID">
    <label for="PW">비밀번호</label>
    <input id="PW" type="password">
    <button>로그인</button>
</form>
```

사용자의 다른 과업을 차단하면서 '확인, 취소' 버튼만 제공하는 경우라면 `role="alertdialog"` 속성이 적절합니다. 사용자가 응답할 필요 없는 내용이라면 `role="alert"` 속성이 적절합니다.

대중적인 브라우저가 `<dialog>` 요소를 충분히 지원하면 `role="dialog"` 속성 대신 `<dialog>` 요소를 사용합니다.



---



## 7. 탐색(`nav`, `role="navigation"`). <a id="nav" href="#nav">#</a>

탐색은 현재 페이지 또는 연결된 페이지를 탐색하는 주요 탐색 블록(보통 링크 집합)입니다. 문서의 '주요 내용'을 탐색하는 경우에 사용하면 적절합니다. 모든 링크 집합이 탐색 블록은 아닙니다.

탐색 블록에 적절한 HTML 요소는 `<nav>` 요소입니다. `role="navigation"` 속성을 사용하기 전에 `<nav>` 요소를 먼저 고려합니다.

탐색 역할을 하는 요소(`<nav>`, `role="navigation"`)가 문서 안에서 유일한 경우 레이블(`aria-labelledby`, `aria-label`) 제공은 선택입니다. 그러나 탐색 역할을 하는 요소가 둘 이상인 경우 고유한 레이블을 제공해야 합니다.

```html
<!-- O: 탐색에 nav 요소를 권장 -->
<nav>
    <h2>글로벌 네비게이션<h2>
    ...
</nav>

<!-- O: 탐색 역할을 하는 요소가 유일한 경우 레이블 생략 가능 -->
<div role="navigation">
    <h2>글로벌 네비게이션<h2>
    ...
</div>

<!-- O: 탐색 역할이 둘 이상인 경우 레이블 제공(nav) -->
<nav aria-labelledby="global-navigation">
    <h2 id="global-navigation">글로벌 네비게이션<h2>
    ...
</nav>
<nav aria-labelledby="notice-pagination">
    <h3 id="notice-pagination">공지사항 페이지네이션<h3>
    ...
</nav>

<!-- O: 탐색 역할이 둘 이상인 경우 레이블 제공(role="navigation") -->
<div role="navigation" aria-labelledby="global-navigation">
    <h2 id="global-navigation">글로벌 네비게이션<h2>
    ...
</div>
<div role="navigation" aria-labelledby="notice-pagination">
    <h3 id="notice-pagination">공지사항 페이지네이션<h3>
    ...
</div>
```

`<nav>` 요소는 섹셔닝 콘텐츠이기 때문에 문서 개요(outline)를 생성합니다. 제목 없는 개요를 만들지 않기 위해 헤딩을 제공합니다. 레이블 요소(예를 들면 헤딩)가 있는 경우 `aria-labelledby` 속성으로 연결합니다. 레이블 요소(예를 들면 헤딩)가 없는 경우 `aria-label` 속성을 사용합니다.



---



## 8. 보충(`aside`, `role="complementary"`). <a id="aside" href="#aside">#</a>

보충은 주요 내용을 보완하는 블록입니다. 문서의 '주요 내용'이 아닙니다. 보충을 제거해도 주요 내용에 변함이 없어야 합니다. 주요 내용에서 보충을 분리한 경우에도 보충은 나름의 의미가 있습니다.

보충으로 적절한 HTML 요소는 `<aside>` 요소입니다. `role="complementary"` 속성을 사용하기 전에 `<aside>` 요소를 먼저 고려합니다.

보충 역할을 하는 요소(`<aside>`, `role="complementary"`)가 문서 안에서 유일한 경우 레이블(`aria-labelledby`, `aria-label`) 제공은 선택입니다. 그러나 보충 역할을 하는 요소가 둘 이상인 경우 고유한 레이블을 제공해야 합니다.

```html
<!-- O: 보충에 aside 요소를 권장 -->
<aside>
    <h2>배너/광고<h2>
    ...
</aside>

<!-- O: 보충 역할을 하는 요소가 유일한 경우 레이블 생략 가능 -->
<div role="complementary">
    <h2>배너/광고<h2>
    ...
</div>

<!-- O: 보충 역할이 둘 이상인 경우 레이블 제공(aside) -->
<aside aria-labelledby="event">
    <h2 id="event">이벤트<h2>
    ...
</aside>
<aside aria-labelledby="advertisement">
    <h2 id="advertisement">배너/광고<h2>
    ...
</aside>

<!-- O: 보충 역할이 둘 이상인 경우 레이블 제공(role="complementary") -->
<div role="complementary" aria-labelledby="event">
    <h2 id="event">이벤트<h2>
    ...
</div>
<div role="complementary" aria-labelledby="advertisement">
    <h2 id="advertisement">배너/광고<h2>
    ...
</div>
```

`<aside>` 요소는 섹셔닝 콘텐츠이기 때문에 문서 개요(outline)를 생성합니다. 제목 없는 개요를 만들지 않기 위해 헤딩을 제공합니다. 레이블 요소(예를 들면 헤딩)가 있는 경우 `aria-labelledby` 속성으로 연결합니다. 레이블 요소(예를 들면 헤딩)가 없는 경우 `aria-label` 속성을 사용합니다.



---



## 9. 의미 없음(`role="none"`). <a id="none" href="#none">#</a>

의미 없음(`role="none"`)을 선언하는 경우 보조기기는 마크업의 의미를 제거 후 내용만 사용자에게 전달합니다. `role="none"` 속성은 `role="presentation"`과 동일하며 `role="presentation"`을 대체합니다. 하위 호환성을 위해 `role="none"` 대신 `role="none presentation"` 형식으로 작성합니다.

HTML을 의미에 맞지 않게 마크업한 경우, 또는 스타일링에 필요한 마크업을 추가한 경우 `role="none"` 속성을 사용할 수 있습니다. 의미에 맞지 않는 마크업과 스타일을 위한 마크업을 권장하지 않기 때문에 이 속성은 절제해야 합니다.

```html
<!-- O: tablist와 tab 사이 li 요소의 의미 제거 -->
<ul role="tablist">
    <li role="none presentation">
        <a href="#home" role="tab" aria-selected="true">홈</a>
    </li>
    <li role="none presentation">
        <a href="#ongoing" role="tab" aria-selected="false">연재</a>
    </li>
    <li role="none presentation">
        <a href="#ranking" role="tab" aria-selected="false">랭킹</a>
    </li>
</ul>
```

의미 없음(`role="none"`)은 숨김(`hidden`, `aria-hidden="true"`) 속성과 다릅니다. 숨김 속성은 요소와 내용을 모두 감추어 버리지만 `role="none"` 속성은 내용을 드러내고 의미만 감춥니다.



---



## 10. 현재 항목(`aria-current="token"`). <a id="aria-current" href="#aria-current">#</a>

`aria-current` 속성은 현재 맥락과 일치하는 항목을 의미합니다. `token` 값은 정해진 값 중 하나만 사용할 수 있음을 의미합니다. 예를 들면 `aria-current` 속성의 `token` 값은 `page|step|location|date|time|true|false(default)` 으로 정해져 있고 이 중 하나만 사용할 수 있습니다.

* `page`: 현재 '페이지'와 일치하는 시각적으로 강조한 링크.
* `step`: 현재 '단계'와 일치하는 시각적으로 강조한 링크.
* `location`: 플로우 차트에서 현재 '위치'와 일치하는 시각적으로 강조한 이미지.
* `date`: 달력에서 현재 '날짜'와 일치하는 날짜.
* `time`: 시간표에서 현재 '시간'과 일치하는 시간.

이 밖에 `true`와 `false` 값도 있습니다. `true` 또는 `false` 값은 구체적으로 어떤 맥락(페이지, 단계, 위치, 날짜, 시간)과 일치하는지 정보를 전달하지 않기 때문에 `page|step|location|date|time` 토큰이 적절하지 않은 맥락에 한하여 사용합니다.

* `true`: 항목이 세트 내 현재 맥락과 일치함.
* `false(default)`: 항목이 세트 내 현재 맥락과 일치하지 않음. 속성 또는 값을 선언하지 않은 경우 초기값.

```html
<!-- O: aria-current="page" 현재 페이지 강조 링크 -->
<nav>
    <h2>글로벌 네비게이션</h2>
    <ul>
        <li><a href="/home" aria-current="page">홈</a></li>
        <li><a href="/ongoing">연재</a></li>
        <li><a href="/ranking">랭킹</a></li>
    </ul>
</nav>

<!-- O: aria-current="step" 현재 단계 강조 링크 -->
<nav>
    <h2>회원 가입</h2>
    <ol>
        <li><a href="/accept-terms" aria-current="setp">약관 동의</a></li>
        <li><a href="/id-password">아이디/비밀번호 생성</a></li>
        <li><a href="/email-authentication">이메일 인증</a></li>
    </ol>
</nav>

<!-- O: aria-current="location" 현재 위치 강조 이미지 -->
<img src="is-payment-success.png" alt="결제 성공?" aria-current="location">
<img src="payment-info.png" alt="결제 내역 안내">
<img src="payment-fail.png" alt="결제 실패 안내">

<!-- O: aria-current="date" 현재 날짜 강조 -->
<td aria-curent="date">12/24(토)</td>
<td>
    <button type="button" aria-curent="date">12/24(토)</button>
</td>

<!-- O: aria-current="time" 현재 시간 강조 -->
<th scope="row" aria-current="time">18:00 ~ 20:00</th>
<td>무한 도전</td>
```

`aria-current` 속성은 `aria-selected` 속성과 다른 의미로 사용하기 때문에 `tablist` 목록 안에서 `aria-selected` 속성을 대체하는 용도로 사용하면 안 됩니다. 그러나 `aria-current` 속성과 `aria-selected` 속성을 함께 선언할 수도 있습니다. 예를 들면 편집 가능한 트리 형식의 목록에서 현재 페이지 항목과 편집을 위해 선택한 항목이 일치하는 경우 함께 선언할 수 있습니다.



---



## 11. 선택 항목(`aria-selected="true|false|undefined"`). <a id="aria-selected" href="#aria-selected">#</a>

`aria-selected` 속성은 단일 또는 다중 선택이 가능한 요소(`role="gridcell|option|row|tab"`)에 한하여 선택 상태를 명시하는 용도로 사용합니다. `role="tab"` 요소에 가장 흔히 사용합니다. 키보드 초점을 받을 수 있는 요소에 적용해야 합니다.

* `undefined(default)`: 속성 또는 값을 선언하지 않은 경우 초기값. 선택할 수 없음.
* `true`: 선택 가능한 요소를 선택했음.
* `false`: 선택 가능한 요소를 선택하지 않았음.

선택 요소에만 `aria-selected="true"` 속성을 적용하면 `aria-selected` 속성을 적용하지 않은 요소는 `aria-selected="undefined"` 상태(선택할 수 없음)가 됩니다. 따라서 선택하지 않은 요소에는 명시적으로 `aria-selected="false"` 속성과 값을 적용합니다.

```html
<!-- O: role="tab" 요소에 선택 상태를 명시 -->
<div role="tablist">
    <a id="mon-anchor" href="#mon" role="tab" aria-selected="true">월</a>
    <a id="tue-anchor" href="#tue" role="tab" aria-selected="false">화</a>
</div>
```

`aria-selected` 속성은 `aria-current` 속성과 다른 의미로 사용하기 때문에 혼동하지 않도록 유의합니다. `aria-selected` 속성은 선택 가능한 요소에, `aria-current` 속성은 현재 맥락과 일치하는 요소에 사용합니다. `aria-selected` 속성은 단일 또는 다중 선택이 가능한 요소(`role="gridcell|option|row|tab"`)에 제한적으로 사용할 수 있습니다. 예를 들면 페이지네이션에서 현재 페이지와 일치하는 링크에는 `aria-selected` 속성이 적절하지 않고 `aria-current` 속성이 적절합니다.



---



## 12. 팝업 있음(`aria-haspopup="token"`). <a id="aria-haspopup" href="#aria-haspopup">#</a>

`aria-haspopup` 속성은 요소에 연결되어 있는 팝업(메뉴, 대화상자 등) 정보를 제공합니다. 팝업은 다른 내용 위에 표시하는 블럭을 의미합니다. 팝업 유형은 `menu`, `listbox`, `tree`, `grid`, `dialog` 으로 제한되어 있기 때문에 의미가 정확하게 일치하는 경우에만 사용해야 합니다. 일반적으로 `menu`와 `dialog` 유형이 빈번하므로 많이 사용할 것입니다.

* `true`: `menu`와 동일한 의미.
* `menu`: `menu(role)` 팝업이 연결됨. `menu(role)`는 링크 목록.
* `dialog`: `dialog(role)` 팝업이 연결됨. `dialog(role)`는 상호작용 요소(버튼 또는 콘트롤)가 포함된 현재 문서의 하위창.
* `listbox`: `listbox(role)` 팝업이 연결됨. `listbox(role)`는 선택 가능한 `option(role)`을 포함한 콤보박스.
* `tree`: `tree(role)` 팝업이 연결됨. `tree(role)`는 하위 `list(role)`을 포함하며 접고 펼칠 수 있음.
* `grid`: `grid(role)` 팝업이 연결됨. `grid(role)`는 행과 열로 구성된 선택 가능한 위젯. 상호작용 가능한 셀이기 때문에 `table(role)`과는 역할이 다름에 유의.
* `false(default)`: 연결된 팝업이 없음을 의미.

```html
<!-- O: aria-haspopup="true|menu" -->
<button type="button" id="menu-button" aria-haspopup="true" aria-controls="menu-list" aria-expanded="false">메뉴</button>
<ul id="menu-list" role="menu" aria-labelledby="menu-button" hidden>
    <li role="none presentation">
        <a href="/completed" role="menuitem">완결</a>
    </li>
    <li role="none presentation">
        <a href="/printed" role="menuitem">단행본</a>
    </li>
</ul>

<!-- O: aria-haspopup="dialog"-->
<a href="#login-dialog" aria-haspopup="dialog">로그인</a>
<section id="login-dialog" role="dialog" aria-labelledby="login-heading" aria-modal="true" hidden>
    <h2 id="login-heading">로그인</h2>
    <form>
        <label for="id-input">아이디</label>
        <input id="id-input" type="text">
        <label for="pw-input">비밀번호</label>
        <input id="pw-input" type="password">
        <button type="submit">로그인</button>
    </form>
</section>
```

연결한 팝업 `role`이 암시적인 경우에도 `aria-haspopup` 속성을 연결할 수 있습니다. 예를 들어 연결된 팝업이 `<dialog>` 요소라면 암시적으로 `role="dialog"` 속성을 지닌 것이므로 `aria-haspopup="dailog"` 속성을 사용할 수 있습니다. 대중적인 브라우저가 `<dialog>` 요소를 충분히 지원하면 `role="dialog"` 속성 대신 `<dialog>` 요소를 사용합니다.



---



## 13. 확장(`aria-expanded="true|false|undefinded"`). <a id="aria-expanded" href="#aria-expanded">#</a>

`aria-expanded` 속성은 제어 대상의 확장 또는 축소 상태를 나타냅니다. 어코디언, 메뉴, 콤보박스, 트리와 같이 하위 그룹(또는 독립적인) 내용을 토글(열기, 닫기)하는 경우에 사용하면 적절합니다. 독립적인 내용을 제어할 때 `aria-controls` 속성을 이용하여 제어 대상을 명시해야 합니다.

* `undefined(default)`: 속성 또는 값을 선언하지 않은 경우 초기값. 제어 대상이 없거나 모두 확장 상태. 확장/축소 제어 불가능.
* `true`: 요소 또는 제어 대상 확장 상태.
* `false`: 요소 또는 제어 대상 축소 상태.

```html
<!-- O: 어코디언 -->
<dt>
    <button type="button" aria-controls="answer-99" aria-expanded="false">보너스 코인은 언제 소진되나요?</button>
</dt>
<dd id="answer-99" hidden>
    <p>만료기한이 짧은 보너스 코인이 일반 코인보다 먼저 소진됩니다.</p>
</dd>

<!-- O: 메뉴 -->
<a id="popular-btn" href="#popular" role="menuitem" aria-haspopup="true" aria-expanded="false">인기</a>
<ul id="popular" role="menu" aria-labelledby="popular-btn" hidden>
    <li role="none presentation">
        <a href="#romance" role="menuitem">로맨스</a>
    </li>
    <li role="none presentation">
        <a href="#drama" role="menuitem">드라마</a>
    </li>
</ul>
```

툴팁(`role="tooltip"`), 알럿(`role="alert"`), 알럿 대화상자(`role="alertdialog"`), 대화상자(`role="dialog"`)와 같이 팝업 스타일을 제어하는 요소에는 `aria-expanded` 속성을 사용하지 않습니다.



---



## 14. 누름(`aria-pressed="tristate"`). <a id="aria-pressed" href="#aria-pressed">#</a>

`aria-pressed` 속성은 토글 버튼(`button`, `role="button"`)이 눌린 상태를 표시합니다. 흔하게 사용하는 속성은 아닙니다. 이 속성을 사용하기 전에 `input[type="radio"]`, `input[type="checkbox"]` 또는 `aria-checked` 또는 `aria-selected` 속성을 먼저 검토하는 것이 좋습니다. 속성 값은 일반적으로 `true` 또는 `false` 두 가지 값을 사용하지만, `tristate` 으로 `true`, `false`, `mixed` 세 가지 상태를 모두 표시할 수도 있습니다. `mixed` 값은 버튼이 제어하는 두 개 이상의 요소 상태값이 모두 `true` 이거나 모두 `false`가 아닌 복합적인 상태를 의미합니다.

* `undefined(default)`: 속성 또는 값을 선언하지 않은 경우 초기값. 누름 상태 표시를 지원하지 않는 버튼.
* `true`: 버튼을 누른 상태.
* `false`: 버튼을 누르지 않은 상태.
* `mixed`: `true` 또는 `false` 값으로 표시할 수 없는 복합적인 상태.

```html
<!-- O: true/false 모드 -->
<button type="button" aria-pressed="true">음소거</button>
<button type="button" aria-pressed="false">음소거</button>

<!-- O: true/false/mixed 모드(이 예제에서 제어 대상이 하나는 true 이고 하나는 false 이다) -->
<button type="button" aria-pressed="mixed" aria-controls="noti-text noti-sound">알림 켜기</button>
<ul>
    <li>
        <input id="noti-text" type="checkbox" checked>
        <label for="noti-text">문자 알림</label>
    </li>
    <li>
        <input id="noti-sound" type="checkbox">
        <label for="noti-sound">소리 알림</label>
    </li>
</ul>

```

토글 버튼이 눌린 상태를 동적 텍스트로 전달하는 경우에는 `aria-pressed` 속성을 사용하지 않습니다. 예를 들어 버튼 설명 텍스트를 `배경음 켜기` 그리고 `배경음 끄기` 형태로 동적으로 변경한다면 `aria-pressed` 속성을 선언하는 것이 오히려 혼란을 초래합니다.



---



## 15. 제어 대상(`aria-controls="ID reference list"`). <a id="aria-controls" href="#aria-controls">#</a>

`aria-controls` 속성은 현재 요소가 제어하는 대상을 명시하는 속성입니다. 주로 `role="tab"`, `aria-haspopup`, `aria-expanded` 속성과 함께 `<button>` 요소가 무엇을 제어하는지 명시합니다. `aria-controls` 속성의 값은 하나 또는 그 이상의 ID 값 입니다. 흔한 경우는 아니지만 ID 값이 여럿인 경우 ID 값을 공백으로 분리합니다.

```html
<!-- O: role="tab" 요소에 aria-controls 속성 사용 -->
<div role="tablist">
    <button type="button" id="mon-anchor" aria-controls="mon" role="tab" aria-selected="true">월</button>
    <button type="button" id="tue-anchor" aria-controls="tue" role="tab" aria-selected="false">화</button>
</div>
<div id="mon" tabindex="0" role="tabpanel" aria-labelledby="mon-anchor">
    월요일 콘텐츠...
</div>
<div id="tue" tabindex="0" role="tabpanel" aria-labelledby="tue-anchor" hidden>
    화요일 콘텐츠...
</div>

<!-- O: aria-haspopup 속성과 함께 aria-controls 속성 사용 -->
<button type="button" aria-haspopup="dialog" aria-controls="login-dialog">로그인</button>
<section id="login-dialog" role="dialog" aria-labelledby="login-heading" aria-modal="true" hidden>
    <h2 id="login-heading">로그인</h2>
    ...
</section>

<!-- O: aria-expanded 속성과 함께 aria-controls 속성 사용 -->
<dt>
    <button type="button" aria-controls="answer-99" aria-expanded="false">보너스 코인은 언제 소진되나요?</button>
</dt>
<dd id="answer-99" hidden>
    <p>만료기한이 짧은 보너스 코인이 일반 코인보다 먼저 소진됩니다.</p>
</dd>
```

`<a>` 요소의 `href` 속성값을 통해 참조(제어) 대상을 명시한 경우 `aria-controls` 속성을 사용하지 않습니다.



---



## 16. 실시간(`aria-live="token"`). <a id="aria-live" href="#aria-live">#</a>

`aria-live` 속성은 실시간으로 내용을 갱신하는 영역을 의미합니다. 값으로 `polite`, `assertive`, `off(default)`를 설정할 수 있으며 갱신하는 내용의 중요도에 따라 선택합니다. 갱신 영역에 `polite`, `assertive`값을 사용하면 갱신하는 순간 보조기기는 사용자에게 내용을 전달합니다. `polite`값은 중요도가 낮은 내용에 사용하여 현재 진행중인 음성 또는 타이핑을 방해하지 않고 뒤늦게 전달합니다. `assertive`값은 중요도가 높은 내용에 사용하여 현재 진행중인 보조기기 작업을 중단하고 갱신 내용을 즉시 사용자에게 전달합니다.

일반적으로 `role` 속성의 값이 `alert`, `alertdialog`, `dialog`인 경우 사용하면 적절합니다. 그 밖에 Ajax 기법을 이용하여 실시간으로 내용을 갱신하는 모든 영역(채팅, 오류, 로그, 상태 표시)에 사용할 수 있습니다.

```html
<!-- O: 대화상자 -->
<form role="dialog" aria-live="polite" aria-modal="true" aria-labelledby="TITLE">
    <h2 id="TITLE">로그인</h2>
    <label for="ID">아이디</label>
    <input id="ID">
    <label for="PW">비밀번호</label>
    <input id="PW" type="password">
    <button>로그인</button>
</form>

<!-- O: 알럿 -->
<div role="alert" aria-live="assertive">
    <p>로그인 후 이용할 수 있습니다.</p>
</div>
```

`assertive`값은 사용자의 현재 작업을 방해할 수 있기 때문에 중요도가 높은 내용을 선별하여 신중하게 적용해야 합니다.



---



## 17. 설명 참조(`aria-labelledby="ID reference list"`). <a id="aria-labelledby" href="#aria-labelledby">#</a>

`aria-labelledby`, `aria-label`, `aria-describedby` 속성은 모두 현재 요소에 설명을 제공하는 속성입니다. `aria-labelledby` 속성은 `ID(s)` 값을 이용하여 '간결한' 내용을 참조(연결)하는 방식으로 설명합니다. 보통 `h1`, `h2`, `h3`, `h4`, `h5`, `h6`, `a`, `button` 요소를 참조하면 적절합니다. `aria-label` 속성과 함께 선언하는 경우 `aria-labelledby` 속성이 우선순위가 높기 때문에 보조기기는 `aria-labelledby` 속성을 설명합니다.

```html
<!-- O: 헤딩 설명 참조 -->
<section role="alert" aria-live="assertive" aria-labelledby="LZ-PATH" hidden>
    <h2 id="LZ-PATH">레진패스란?</h2>
    <p>이 작품의 유료 에피소드 열람 시 자동으로 구매합니다.</p>
</section>

<!-- O: 링크 설명 참조 -->
<a id="LZ-PATH" href="#LZ-PATH-TEXT">레진패스란?</a>
<div id="LZ-PATH-TEXT" aria-live="polite" aria-labelledby="LZ-PATH" hidden>
    <p>이 작품의 유료 에피소드 열람 시 자동으로 구매합니다.</p>
</div>
```

`aria-labelledby` 속성으로 숨김 처리한 설명을 참조하면 안 됩니다. 참조가 불가능한 설명은 `aria-label` 속성을 사용합니다. 장황한 설명을 참조하면 안 됩니다. 장황한 설명은 `aria-descibedby` 속성을 사용합니다.



---



## 18. 설명(`aria-label="string"`). <a id="aria-label" href="#aria-label">#</a>

`aria-labelledby`, `aria-label`, `aria-describedby` 속성은 모두 현재 요소에 설명을 제공하는 속성입니다. `aria-label` 속성은 값에 '간결한' 설명(string)을 직접 제공합니다. 가능한 한 `aria-labelledby` 속성을 사용하는 것이 좋습니다. `aria-label` 속성은 현재 요소를 설명할 다른 참조(연결) 요소가 없는 경우에만 사용합니다. `aria-labelledby` 속성과 함께 선언하는 경우 `aria-label` 속성이 우선순위가 낮기 때문에 보조기기는 `aria-labelledby` 속성을 설명합니다.



```html
<form>
    <input type="search" aria-label="웹툰 검색">
    <button>검색</button>
</form>
```

`aria-label` 속성을 장황하게 작성하면 안 됩니다. 장황한 설명은 `aria-descibedby` 속성을 사용합니다.



---



## 19. 자세한 설명 참조(`aria-describedby="ID reference list"`). <a id="aria-describedby" href="#aria-describedby">#</a>

`aria-labelledby`, `aria-label`, `aria-describedby` 속성은 모두 현재 요소에 설명을 제공하는 속성입니다.

```html
```



---



## 99. 참고 문서 <a id="references" href="#references">#</a>

* [HTML 5.2](https://www.w3.org/TR/html52/)
* [WAI-ARIA 1.1](https://www.w3.org/TR/wai-aria/)
* [Using ARIA](https://www.w3.org/TR/using-aria/)
* [ARIA in HTML](https://www.w3.org/TR/html-aria/)
* [WAI-ARIA Authoring Practices 1.1](https://www.w3.org/TR/wai-aria-practices/)
* [ARIA Landmarks Example](https://www.w3.org/TR/wai-aria-practices/examples/landmarks/)



---



## License
Under MIT License. Copyright &copy; Lezhin.
