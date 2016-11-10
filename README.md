# Xpress Engine Front-end Guide


## XE Core
### XE.Lang
#### XE.Lang.trans( id [, parameter] )
등록되어 있는 다국어를 리턴해줍니다.
##### id (string)
다국어가 정의된 key값을 지정합니다. ( 필수 요소 )
##### parameter (object)
object타입으로 2번째 인자에 사용하면 해당 번역에 지정된 문자열을 치환합니다.

```php
//langs.php
<?php
return [
      'name' => [
        'ko' => '이름'
        'en' => 'Name'
      ],
      'email' => [
        'ko' => '이메일',
        'en' => 'E-mail'
      ],
      'msgHello' => [
        'ko' => '안녕하세요. :msg',
        'en' => 'Hello. :msg'
      ]
];
```
```javascript
//javascript
var name = XE.Lang.trans('xe::name');
var email = XE.Lang.trans('xe::email');
var msg = XE.Lang.trans('xe::msgHello', {msg: 반갑습니다.});
console.log(name) // 이름 or Name
console.log(email) // 이메일 or E-mail
console.log(msg) // 안녕하세요. 반갑습니다.
```

### XE.Progress

#### XE.Progress.start()
Progress bar를 생성하는 UI를 화면에 노출합니다. 
```javascript
XE.Progress.start(); // progress bar 생성
```
#### XE.Progress.done()
Progress bar를 생성하는 UI를 종료합니다.
```javascript
XE.Progress.done(); // progress bar 제거
```


### XE.Request

#### XE.Request.get( url [, data] [, callback] [, dataType] )
서버로부터 데이터를 전달 받습니다.
##### url (string)
요청보낼 URL 값
##### data (object or string)
서버로 전송할 파라미터
##### callback (function)
요청 성공시 실행될 콜백
##### dataType (string)
서버로부터 전송되는 데이터의 타입 (json, xml, html, text, script)

```javascript
XE.Request.get('/item/3', function(data) {
      console.log(data);
});
```

#### XE.Request.post( url [, data] [, callback] [, dataType] )
##### url (string)
요청보낼 URL 값
##### data (object or string)
서버로 전송할 파라미터
##### callback (function)
요청 성공시 실행될 콜백
##### dataType (string)
서버로부터 전송되는 데이터의 타입 (json, xml, html, text, script)
```javascript
XE.Request.post('/item', {name: 'xe'},  function(data) {
      console.log(data);
}, 'json');
```
  
#### XE.ajax( url [, settings] ) or XE.ajax( [settings] )
XE.ajax는 jQeury의 $.ajax를 wrapping한 형태를 취하고 있습니다. settings에 사용되는 옵션들은 jQuery의 옵션들을 그대로 사용하실 수 있습니다.
##### url (string)
요청보낼 URL 값
##### settings (object)
* type (string) http method 'get' | 'post' 등
* data (object) 서버로 전송할 파라미터
* dataType (string) 서버로부터 전송되는 데이터의 타입 (json, xml, html, text, script)
* success (function) 요청 성공시 실행될 콜백
* error (function) 요청 실패시 실행될 콜백

```javascript
XE.ajax('/item', {
      type: 'get',
      dataType: 'json',
      data: {
        id: 'p3'
      },
      success: function(data) {
        console.log(data);
      },
      error: function(jqXHR, textStatus, errorThrown) {
        console.log(jqXHR, textStatus, errorThrown);
      }
});
```

### XE form
XE form은 마크업된 form요소의 attribute를 통해 ajax를 사용하는 방법입니다. 우선 XE form을 사용하기 위해서는 xe-form.js 스크립트를 로드해야 합니다.

```php
//blade파일(php)에서 로드할 경우
{{ XeFrontend::js('assets/core/xe-ui-component/js/xe-form.js')->appendTo('body')->load() }}

```
```html
<-- html에서 로드할 경우 -->
<script type='text/javascript' src='assets/core/xe-ui-component/js/xe-form.js'></script>
```

xe-form.js파일을 로드한 상태에서 form마크업시 **data-submit='xe-ajax'** attribute를 사용하게 되면 해당 form이 submit될 때 XE.ajax가 실행됩니다.

####Attributes
* data-submit : XE form을 사용하기 위한 **필수** 요소
* action : 요청할 url 정보
* method : http method POST | GET
* data-callback : 요청이 정상 응답일 경우 실행될 callback 콜백으로 사용할 자바스크립트의 별도 구현이 필요
* data-validate (boolean) : 요청전 폼 요소의 유효성 체크를 합니다. 유효성 체크를 하려면 XE UI Components의 XE.validate의 내용을 폼요소에 적용해야 합니다. true|false

```html
<!-- XE form sample -->
<form action="/users" method="POST" data-submit="xe-ajax" data-callback="test" data-validate='true'>
  <div class="xe-form-group">
    <label for="id">ID</label>
    <input type="text" class="xe-form-control" id="id" />
  </div>
  <div class="xe-form-group">
    <label for="password">Password</label>
    <input type="password" class="xe-form-control" id="password" />
  </div>
</form>
```

```javascript
//callback sample
function test(response) {
  console.log(response);
  alert('success');
}
```

### XE.page(url, target, options, callback)
target영역에 html을 로드하여 화면에 랜더링합니다. response로 html 및 js, css파일들의 경로를 전달 받습니다.
#### 동작 순서
1. js, css파일 로드
2. html 로드
3. callback 실행 

####arguments
##### url (string)
ajax가 호출될 url
##### target (string)
html이 append될 selector 
##### options (object)
* data (object) 전송 파라미터
* type (string) http method 'get'|'post'
* addType (string) target에 response html을 넣어주는 방식의 타입 `append`, `prepend`, `before`, `after`. 옵션을 명시하지 않을 경우 target영역에 html을 덮어 넣습니다.
  
##### callback (function)
html append이후에 실행될 callback

#### 마크업에 `data-*` attruibute를 이용한 XE.page 사용 방법
xe.page.js파일을 로드하면 `data-toggle="xe-page"` attribute를 사용한 DOM에 click이벤트를 바인딩 합니다. 

* `assets/core/common/xe.page.js`의 파일을 로드합니다.
* 클릭되는 DOM에 `data-toggle='xe-page'` attribute를 명시하여야 합니다.
* href or data-url에 ajax를 요청할 url정보를 명시합니다.
* data-target으로 append할 영역의 selector를 명시합니다.
* data-callback으로 callback명을 명시합니다.
* data-params로 요청시 전송할 파라미터 정보를 명시합니다. (JSON string)

```html
<a href="/api/test" 
    data-toggle="xe-page" 
    data-params="{'param1':'value1'}" 
    data-target="#target" 
    data-callback="callbackFunc">[XE.page 실행]</a>
```

### XE.pageModal(url, options, callback)
xeModal을 실행하여 html을 해당 modal영역에 랜더링합니다. response로 html 및 js, css파일들의 경로를 전달 받습니다.

#### 동작 순서
1. js, css파일 로드
2. html로드
3. callback 실행
4. xeModal 실행

####arguments
##### url (string)
ajax가 호출될 url
##### options (object)
* data (object) 전송 파라미터
* type (string) http method 'get'|'post'
  
##### callback (function)
html append이후에 실행될 callback

#### 마크업에 `data-*` attruibute를 이용한 XE.pageModal 사용 방법
xe.page.js파일을 로드하면 `data-toggle="xe-page-modal"` attribute를 사용한 DOM에 click이벤트를 바인딩 합니다. 

* `assets/core/common/xe.page.js`의 파일을 로드합니다.
* 클릭되는 DOM에 `data-toggle='xe-page-modal'` attribute를 명시하여야 합니다.
* href or data-url에 ajax를 요청할 url정보를 명시합니다.
* data-callback으로 callback명을 명시합니다.
* data-params로 요청시 전송할 파라미터 정보를 명시합니다. (JSON string)

```html
<a href="/api/test" 
    data-toggle="xe-page-modal" 
    data-params="{'param1':'value1'}" 
    data-callback="callbackFunc">[XE.pageModal 실행]</a>
```

### XE.validate( $form )
해당 폼 요소에 있는 값들의 유효성을 체크합니다. 마크업에 있는 element의 data-valid attribute에 정의된 유효성을 체크합니다. 유효성 체크를 하고자 하는 내용을 '|'구분하여 지정하면 여러개의 유효성을 체크하게되고 유효성이 통과하지 못할 경우 메시지를 노출합니다.

####data-rule-alert-type
유효성 체크를 통과하지 못할 경우 보여질 메시지형태를 정의합니다. 메시지형태는 toast, form 2가지 요소가 있습니다.
* toast
  - XE.toast 팝업의 형태로 메시지가 노출됩니다.
* form
  - 해당 필드 요소하단에 메시지가 노출됩니다.

####data-valid
* required
  - 필수 요소일 경우 사용합니다.
* checked:min-max
  - checkbox, raido 타입에 사용됩니다.
  - **첫번째 엘리먼트**에만 해당 요소가 정의되어야 합니다.
  - min, max는 number 타입으로 지정합니다. radio button에서는 필수 체크시 **checked:1**로 표기 합니다.
* alpha
  - 알파벳으로만 사용되는 필드 값을 체크합니다.
* alphanum
  - 알파벳 또는 숫자 값을 체크합니다.
* min
  - 최소 입력 글자를 체크합니다.
* max
  - 최대 입력 글자를 체크합니다
* email
  - 이메일 형식인지 체크합니다.
* url
  - url형식으로 입력되었는지 체크합니다.
* numeric
 - 숫자값만 입력되었는지 체크합니다.
* between:min,max
 - 필드 값이 최소, 최대에 만족하는지 체크합니다.

```html
<!-- XE form sample -->
<form id='form' action="/users" method="POST" data-rule-alert-type="toast">
    <div class="xe-form-group">
        <label for="id">ID</label>
        <input type="text" name="id" class="xe-form-control" id="id" data-valid='required|alphanum' />
    </div>
    <div class="xe-form-group">
        <label for="password">Password</label>
        <input type="password" name="password" class="xe-form-control" id="password" data-valid='required|alphanum' />
    </div>
    <div>
        <label for='chk1' class="checkbox-inline"><input name="check[]" id='chk1' type="checkbox" value='apple' data-valid='checked:1-3' />사과</label>
        <label for='chk2' class="checkbox-inline"><input name="check[]" id='chk2' type="checkbox" value='grape' />포도</label>
        <label for='chk3' class="checkbox-inline"><input name="check[]" id='chk3' type="checkbox" value='strawberry' />딸기</label>
        <label for='chk4' class="checkbox-inline"><input name="check[]" id='chk4' type="checkbox" value='lemon' />레몬</label>
    </div>
</form>
```
```javascript
XE.formValidate($('#form'));
```

## XE UI Components

### toast popup
#### XE.toast( type, message )
토스트 팝업을 생성하여 메시지를 보여줍니다.
##### type (string)
타입은 **danger** | **positive** | **warning** | **success** | **fail** | **error** | **info**로 정의되어 있으며 생성되는 팝업의 스킨을 변경하여 줍니다.
##### message (string)
toast popup 생성시 보여줄 메시지를 지정합니다.
```javascript
XE.toast('success', '토스트 팝업 생성 성공!');
```

### dropdown
#### $(selector).xeDropdown()
dropdown메뉴를 생성하는 UI 컴포넌트입니다. html마크업을 통해서 해당 컴포넌트 기능을 사용할 경우에는 `data-toggle="xe-dropdown"` 속성을 버튼에 사용해 주어야 합니다. 버튼에 해당 속성을 사용해 주게 되면 이벤트가 자동으로 바인딩되어 버튼 기능이 활성화 됩니다.

##### Basic select
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

##### Dropdown
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

##### Label select
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
##### outline-off
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
### modal
#### $(selector).xeModal( options )
modal창을 생성하는 UI 컴포넌트입니다. html마크업을 통해서 해당 컴포넌트 기능을 사용할 경우에는 `data-toggle="xe-modal"` 속성을 버튼에 사용해 주어야 합니다. 버튼에 해당 속성을 사용해 주게 되면 이벤트가 자동으로 바인딩되어 버튼 기능이 활성화 됩니다.
##### options (object)
* backdrop
* keyboard
* show
* remote

모달의 기본 구조는 `.xe-modal-header`, `.xe-modal-body`, `.xe-modal-footer`로 구성되어 있습니다.

```html
<div class="xe-example">
    <div class="xe-modal fade" id="modal" >
        <div class="xe-modal-dialog">
            <div class="xe-modal-content">
                <div class="xe-modal-header">
                    <button type="button" class="btn-close" data-dismiss="xe-modal" aria-label="Close"><i class="xi-close"></i></button>
                    <strong class="xe-modal-title">Modal title</strong>
                </div>
                <div class="xe-modal-body">
                    <p>
                        modal-body ...
                    </p>
                </div>
                <div class="xe-modal-footer">
                    <button type="button" class="xe-btn xe-btn-secondary" data-dismiss="xe-modal">취소</button>
                    <button type="button" class="xe-btn xe-btn-primary" data-dismiss="xe-modal">저장</button>
                </div>
            </div>
        </div>
    </div>
</div>
```

`.xe-modal-lg`, `.xe-modal-sm` 클래스를 통해 모달 사이지를 지정할 수 있습니다.

```html
<div class="xe-modal fade" id="modal-sm">
    <div class="xe-modal-dialog xe-modal-sm">
        <div class="xe-modal-content">
            <div class="xe-modal-header">
                <button type="button" class="btn-close" data-dismiss="xe-modal" aria-label="Close"><i class="xi-close"></i></button>
                <strong class="xe-modal-title">Modal title</strong>
            </div>
            <div class="xe-modal-body">
                <p>
                    modal-body ...
                </p>
            </div>
            <div class="xe-modal-footer">
                <button type="button" class="xe-btn xe-btn-secondary" data-dismiss="xe-modal">취소</button>
                <button type="button" class="xe-btn xe-btn-primary" data-dismiss="xe-modal">저장</button>
            </div>
        </div>
    </div>
</div>
<div class="xe-modal fade" id="modal-lg">
    <div class="xe-modal-dialog xe-modal-lg">
        <div class="xe-modal-content">
            <div class="xe-modal-header">
                <button type="button" class="btn-close" data-dismiss="xe-modal" aria-label="Close"><i class="xi-close"></i></button>
                <strong class="xe-modal-title">Modal title</strong>
            </div>
            <div class="xe-modal-body">
                <p>
                    modal-body ...
                </p>
            </div>
            <div class="xe-modal-footer">
                <button type="button" class="xe-btn xe-btn-secondary" data-dismiss="xe-modal">취소</button>
                <button type="button" class="xe-btn xe-btn-primary" data-dismiss="xe-modal">저장</button>
            </div>
        </div>
    </div>
</div>
```

modal생성시 자바스크립트 `$(selector).xeModal()`를 호출하여 modal을 생성합니다. 
```javascript
$('#modal').xeModal();
```
### tooltip
#### $(selector).xeTooltip( options )
tooltip을 생성하는 UI 컴포넌트입니다. html마크업을 통해서 해당 컴포넌트 기능을 사용할 경우에는 `data-toggle="xe-tooltip"` 속성을 버튼에 사용해 주어야 합니다. 버튼에 해당 속성을 사용해 주게 되면 이벤트가 자동으로 바인딩되어 버튼 기능이 활성화 됩니다.
##### options (object)
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
### lightbox
#### $(selector).lightbox()

```html
<div class="images" data-toggle="xe-lightbox" data-selector="img">
   <img src="sample/img/@sample_img.jpg">
   <img src="sample/img/@sample_img2.jpg">
   <img src="sample/img/@sample_img3.jpg">
   <img src="sample/img/@sample_img4.jpg">
   <img src="sample/img/@sample_img5.jpg">
   <img src="sample/img/@sample_img6.jpg">
   <img src="sample/img/@sample_img7.jpg">
</div>
```
```javascript
$('.images > img').lightbox();
```


## Common
### dynamicLoadManager
DynamicLoadManager는 script, css파일등을 비동기로 로드하고 스크립트 중복 로드를 방지합니다.

#### DynamicLoadManager.jsLaod( url [, load] [, error] )
javascript파일을 로드하고 요청 성공시 load콜백을 실행합니다.
##### url (string)
로드할 스크립트의 url주소
##### load (function)
로드 성공시 호출될 콜백
##### error (function)
로드 실패시 호출될 콜백
```javascript
DynamicLoadManager.jsLoad('assets/common/utils.js', function() {
    console.log('loaded');
}, function() {
    console.error('load error!');
});
```

#### DynamicLoadManager.jsLoadMultiple( url[] [, callbackObj] )
여러개의 javascript파일을 순차적으로 로드하고 요청 성공시 각각 load콜백을 실행합니다. 모든 파일이 로드되면 complete를 호출합니다.
##### url (string)
##### callbackObj (object)
* load (function)
* error (function)
* complete (function)

```javascript
  DynamicLoadManager.jsLoadMultiple([
      '/assets/test/test1.js',
      '/assets/test/test2.js',
      '/assets/test/test3.js',
      '/assets/test/test4.js',
      '/assets/test/test5.js'
  ], {
      load: function() {
        console.log('loaded');
      },
      error: function() {
        console.log('error');
      },
      complete: function() {
        console.log('complete');
      }
  });
```

#### DynamicLoadManager.cssLoad( url [, load] [, error] )
css파일을 로드하고 요청 성공시 load콜백을 실행합니다.
##### url (string)
로드할 스크립트의 url주소
##### load (function)
로드 성공시 호출될 콜백
##### error (function)
로드 실패시 호출될 콜백
```javascript
  DynamicLoadManager.cssLoad('/assets/test/test.css', function() {
    console.log('loaded');
  });
```
### utils
#### Utils.asset( url )
##### url (string)
```javascript
var url = Utils.asset('/asset/test');
console.log(url) //http://localhost:port/asset/test
```