# 레진 WAI-ARIA 가이드라인

[WAI-ARIA](https://www.w3.org/TR/wai-aria-1.1/)는 HTML의 접근성 문제를 보완하는 W3C 명세입니다. WAI-ARIA는 HTML 요소에 `role` 또는 `aria-*` 속성을 추가하여 콘텐츠의 '역할, 상태, 속성' 정보를 보조기기에 제공합니다.
```
<!-- 레진엔터테인먼트에서 사용하고 있는 WAI-ARIA 예제 -->

<!-- 역할 -->
<element role="tablist">
<element role="tab">
<element role="tabpanel">
<element role="alert">
<element role="tooltip">
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

## 2. 탭 목록, 탭, 탭 패널 콘텐츠.

탭은 스타일을 의미하는 것이 아니라 콘텐츠에 색인을 제공하는 구조(tablist, tab, tabpanel)를 의미합니다. 따라서 사이트 탐색 도구에 해당하는 요소는 `nav > h2 + ul` 또는 `aside > h2 + ul` 구조로 마크업 합니다.

```
<!-- O -->
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

<!-- O -->
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
