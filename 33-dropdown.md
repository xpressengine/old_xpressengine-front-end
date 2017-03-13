# 3.3 Dropdown
---

## $(selector).xeDropdown()
dropdown메뉴를 생성하는 UI 컴포넌트입니다. html마크업을 통해서 해당 컴포넌트 기능을 사용할 경우에는 `data-toggle="xe-dropdown"` 속성을 버튼에 사용해 주어야 합니다. 버튼에 해당 속성을 사용해 주게 되면 이벤트가 자동으로 바인딩되어 버튼 기능이 활성화 됩니다.

### Basic select
브라우져 기본 <select>로 열리게 되어 모바일에서도 사용성을 높여주며 option 선택 시 자바스크립트 코드와 함께 실행됩니다.
```html
<div class="xe-select-box xe-btn">
    <label>xe-select-box 1</label>
    <select>
    <option>xe-select-box 1</option>
    <option>xe-select-box 2</option>
    <option>xe-select-box 3</option>
    <option>xe-select-box 4</option>
    </select>
</div>
```

### Dropdown
data 속성을 통해서, 드롭다운 부모 목록 항목에 .open 클래스 토글링으로 드롭다운 메뉴를 토글합니다.

```html
<!-- html -->
<div class="xe-dropdown">
    <button class="xe-btn" type="button" data-toggle="xe-dropdown">xe-dropdown 1</button>
    <ul class="xe-dropdown-menu">
        <li class="on"><a href="#">xe-dropdown 1</a></li>
        <li><a href="#">xe-dropdown 2</a></li>
        <li><a href="#">xe-dropdown 3</a></li>
        <li><a href="#">xe-dropdown 4</a></li>
    </ul>
</div>
```

### Label select
2개 이상의 option을 선택할 수 있으며, option 리스트가 많은 경우를 대비하여 검색 기능을 제공합니다.
```html
<div class="xe-select-label">
    <div class="label-input">
        <ul>
            <li>
                <span class="label-choice">ie9<button type="button"><i class="xi-close"></i></button></span>
            </li>
            <li>
                <span class="label-choice">safari<button type="button"><i class="xi-close"></i></button></span>
            </li>
            <li>
                <span class="label-choice">chrome<button type="button"><i class="xi-close"></i></button></span>
            </li>
            <li><input type="text" class="search-label"></li>
        </ul>
    </div>
    <div class="label-list">
        <div class="label-division">
            <strong>그룹핑 제목(그룹이 하나일 경우 제외)</strong>
            <ul>
                <li><a href="#">IE9</a></li>
                <li><a href="#">IE10</a></li>
            </ul>
        </div>
        <div class="label-division">
            <strong>그룹핑 제목(그룹이 하나일 경우 제외)</strong>
            <ul>
                <li><a href="#">safari</a></li>
                <li><a href="#">chrome</a></li>
            </ul>
        </div>
    </div>
</div>
```
### outline-off
.outline-off 클래스를 추가하여 BG 없어 border로만 이루어져 있는 dropdown 스타일을 사용할 수 있습니다.
```html
<div class="xe-select-box xe-btn outline-off">
    <label>xe-select-box 1</label>
    <select>
    <option>xe-select-box 1</option>
    <option>xe-select-box 2</option>
    <option>xe-select-box 3</option>
    <option>xe-select-box 4</option>
    </select>
</div>

<div class="xe-dropdown outline-off">
    <button class="xe-btn" type="button" data-toggle="xe-dropdown">xe-dropdown 1</button>
    <ul class="xe-dropdown-menu">
    <li><a href="#" class="on">xe-dropdown 1</a></li>
    <li><a href="#">xe-dropdown 2</a></li>
    <li><a href="#">xe-dropdown 3</a></li>
    <li><a href="#">xe-dropdown 4</a></li>
    </ul>
</div>
```

```javascript
//javascript
$('[data-toggle=xe-dropdown]').xeDropdown();
```
