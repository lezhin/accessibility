# 레진 WAI-ARIA 가이드라인

[WAI-ARIA](https://www.w3.org/TR/wai-aria-1.1/)는 HTML의 접근성 문제를 보완하는 W3C 명세입니다. WAI-ARIA는 HTML 요소에 `role` 또는 `aria-*` 속성을 추가하여 콘텐츠의 '역할, 상태, 속성' 정보를 보조기기에 제공합니다.
```
<!-- 레진엔터테인먼트에서 사용하고 있는 WAI-ARIA 예제 -->

<!-- 역할 -->
<element role="tablist">
<element role="tab">
<element role="tabpanel">
<element role="tooltip">
<element role="alert">
<element role="alertdialog">
<element role="dialog">
<element role="complementary">
<element role="none">

<!-- 상태 -->
<element aria-selected="true">
<element aria-pressed="true">
<element aria-haspopup="true">
<element aria-expanded="true">
<element aria-checked="true">

<!-- 속성 -->
<element aria-live="polite">
<element aria-labelledby="id reference list">
<element aria-label="오늘의 만화">
<element aria-describedby="id reference list">
<element aria-controls="id reference list">
<element aria-current="page">
```



## 1. HTML을 의미있게 작성한다.
대부분의 WAI-ARIA 명세는 HTML 요소와 속성을 흉내내는 것입니다. 올바른 HTML을 사용한다면 WAI-ARIA 사용을 최소화할 수 있습니다. WAI-ARIA를 사용하기에 앞서 HTML을 의미있게 사용했는지 충분히 검토합니다.

```
<!-- X -->
<a href="#" role="button">

<!-- O -->
<button type="button">
```
보조기기는 두 가지 예제를 모두 '버튼'으로 간주할 것입니다. 그러나 첫 번째 예제의 경우 브라우저는 문맥 메뉴를 통해 링크와 관련된 기능(새 탭에서 링크 열기, 링크 주소 복사 등)을 제공하게 되고 사용자를 혼란스럽게 합니다. 또한 첫 번째 예제에서 '버튼' 이라는 설명을 들은 보조기기 사용자는 '스페이스'키를 눌러 버튼 기능을 사용하려고 시도할 수 있습니다. 하지만 `a` 요소는 '엔터' 키 만으로 실행할 수 있습니다. `button` 요소는 '엔터' 키와 '스페이스' 키로 실행할 수 있기 때문에 `a` 요소로부터 '버튼' 이라는 설명을 전해들은 보조기기 사용자를 혼란스럽게 합니다. 결국 올바른 HTML의 선택은 사용자 경험과 접근성 측면에서 모두 중요합니다.



## 2. 탭 목록, 탭, 탭 패널.

탭은 스타일을 의미하는 것이 아니라 콘텐츠에 색인을 제공하는 구조(tablist, tab, tabpanel)를 의미합니다. 사이트 탐색 도구에 해당하는 요소는 `nav > h2 + ul` 또는 `aside > h2 + ul` 구조로 마크업 합니다.

```
<!-- O: 앵커 형식 탭 -->
<div class="weekly">
    <div role="tablist">
        <a id="mon-anchor" href="#mon" role="tab" aria-selected="true">월</a>
        <a id="tue-anchor" href="#tue" role="tab">화</a>
    </div>
    <div id="mon" tabindex="0" role="tabpanel" aria-labelledby="mon-anchor">
        월요일엔 빨간 장미를...
    </div>
    <div id="tue" tabindex="0" role="tabpanel" aria-labelledby="tue-anchor">
        화요일엔 노란 장미를...
    </div>
</div>

<!-- O: 버튼 형식 탭 -->
<div class="weekly">
    <div role="tablist">
        <button type="button" id="mon-anchor" aria-controls="mon" role="tab" aria-selected="true">월</button>
        <button type="button" id="tue-anchor" aria-controls="tue" role="tab">화</button>
    </div>
    <div id="mon" tabindex="0" role="tabpanel" aria-labelledby="mon-anchor">
        월요일엔 빨간 장미를...
    </div>
    <div id="tue" tabindex="0" role="tabpanel" aria-labelledby="tue-anchor">
        화요일엔 노란 장미를...
    </div>
</div>
```



## 3. 툴팁.

툴팁은 앵커 또는 폼 콘트롤 요소에 대한 참고용 콘텐츠입니다. 보통 마우스 오버 또는 키보드 초점을 받으면 표시하는 내용이지만 화면에 항상 표시할 수도 있습니다. 툴팁 요소에 `role="tooltip"` 속성으로 명시할 수 있습니다. 툴팁을 유발하는 앵커 또는 콘트롤에 `aria-describedby="ID reference list"` 속성을 명시하여 연결해야 합니다. `role="alert"` 또는 `role="alertdialog"` 또는 `role="dialog"` 콘텐츠와 혼동하지 않도록 유의합니다.

```
<!-- O: 인풋 툴팁 -->
<label for="tel">전화번호</label>
<input id="tel" type="tel" aria-describedby="TIP-TEL">
<p id="TIP-TEL" role="tooltip" hidden>하이픈(-) 없이 숫자만 입력.</p>

<!-- O: 버튼 툴팁 -->
<button aria-describedby="TIP-DEL">삭제</button>
<p id="TIP-DEL" role="tooltip" hidden>삭제 후 복원할 수 없음.</p>
```


## 4. 알럿, 알럿 대화상자.

알럿은 일시적으로 민감한 정보를 사용자에게 전달하는 콘텐츠입니다. 운영체제 또는 브라우저에서 제공하는 시스템 알럿 대신 HTML 마크업으로 스타일 처리한 알럿을 제공할 수 있습니다. 알럿 발생 시 보조 기기에 실시간으로 알림을 전달하려면 `aria-live="assertive"` 속성을 명시해야 합니다. 초점을 받을 필요가 없는 알럿은 `role="alert"` 으로 처리합니다.

콘트롤(input, textarea, select, button) 또는 링크(a)와 같이 사용자 인터렉션을 포함한 알럿이라면 `role="alertdialog"` 으로 처리합니다. 알럿 대화상자에는 `aria-labelledby="ID reference list"` 그리고 `aria-describedby="ID reference list"` 속성으로 알럿의 제목과 설명을 연결해야 합니다. 알럿 대화상자를 표시할 때 모달 윈도우 형식으로 표시하고 키보드 초점을 대화상자 내부 콘트롤(예를 들면 '확인' 버튼)으로 옮겨야 합니다. 초점은 대화상자 안에서 벗어나지 않아야 합니다.

```
<!-- O: 알럿 -->
<div role="alert" aria-live="assertive">
    <p>유효한 이메일 주소가 아닙니다.</p>
</div>

<!-- O: 알럿 대화상자 -->
<div role="alertdialog" aria-live="assertive" aria-labelledby="TITLE" aria-describedby="DESCRIPTION">
    <h2 id="TITLE">레진패스 안내</h2>
    <p id="DESCRIPTION">이 작품의 유료 에피소드 열람 시 자동으로 구매합니다. 레진패스를 적용하시겠습니까?</p>
    <button type="button">레진패스 적용</button>
    <button type="button">취소</button>
</div>
```

대중적인 브라우저가 `<dialog>` 요소를 충분히 지원하면 `role="alertdialog"` 또는 `role="dialog"` 속성 대신 `<dialog>` 요소를 사용하는 것이 바람직합니다.

