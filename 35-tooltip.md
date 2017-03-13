#3.5 Tooltip
---
## $(selector).xeTooltip( options )
tooltip을 생성하는 UI 컴포넌트입니다. html마크업을 통해서 해당 컴포넌트 기능을 사용할 경우에는 `data-toggle="xe-tooltip"` 속성을 버튼에 사용해 주어야 합니다. 버튼에 해당 속성을 사용해 주게 되면 이벤트가 자동으로 바인딩되어 버튼 기능이 활성화 됩니다.
### options (object)
* animation (boolean)
* container (string|false)
* delay (number|object)
* html (boolean)
* placement (string|function)
* selector (string)
* template (string)
* title (string|element|function)
* trigger (string)

```html
<button type="button" class="xe-btn xe-btn-success" data-toggle="xe-tooltip" data-placement="left" title="Tooltip on left">xe-tooltip on left</button>
```
4가지 방향(위, 오른쪽, 아래, 왼쪽)으로 노출합니다.
```html
<div class="xe-tooltip left" role="tooltip">
    <div class="xe-tooltip-arrow"></div>
    <div class="xe-tooltip-inner">
    Tooltip on the left
    </div>
</div>
<div class="xe-tooltip top" role="tooltip">
    <div class="xe-tooltip-arrow"></div>
    <div class="xe-tooltip-inner">
    Tooltip on the top
    </div>
</div>
<div class="xe-tooltip bottom" role="tooltip">
    <div class="xe-tooltip-arrow"></div>
    <div class="xe-tooltip-inner">
    Tooltip on the bottom
    </div>
</div>
<div class="xe-tooltip right" role="tooltip">
    <div class="xe-tooltip-arrow"></div>
    <div class="xe-tooltip-inner">
    Tooltip on the right
    </div>
</div>
```
title 속성을 통해 totltip 내용을 노출합니다.
```html
<button type="button" class="xe-btn xe-btn-success" data-toggle="xe-tooltip" data-placement="left" title="Tooltip on left">xe-tooltip on left</button>
<button type="button" class="xe-btn xe-btn-success" data-toggle="xe-tooltip" data-placement="top" title="Tooltip on top">xe-tooltip on top</button>
<button type="button" class="xe-btn xe-btn-success" data-toggle="xe-tooltip" data-placement="bottom" title="Tooltip on bottom">xe-tooltip on bottom</button>
<button type="button" class="xe-btn xe-btn-success" data-toggle="xe-tooltip" data-placement="right" title="Tooltip on right">xe-tooltip on right</button>
```
javascript에서 xeTooltop을 호출하여 실행합니다.
```javascript
$('[data-toggle="xe-tooltip"]').xeTooltip();
```
