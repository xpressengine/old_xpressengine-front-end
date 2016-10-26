# Xpress Engine Front-end Guide


## XE Core
### 1. XE.Lang
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

### 2. XE.Progress

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


### 3. XE.Request

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

## XE UI Components
### 1. toast popup
#### XE.toast( type, message )
토스트 팝업을 생성하여 메시지를 보여줍니다.
##### type (string)
타입은 **danger** | **positive** | **warning** | **success** | **fail** | **error** | **info**로 정의되어 있으며 생성되는 팝업의 스킨을 변경하여 줍니다.
##### message (string)
toast popup 생성시 보여줄 메시지를 지정합니다.
```javascript
XE.toast('success', '토스트 팝업 생성 성공!');
```

### 2. dropdown
#### $(selector).xeDropdown()
dropdown메뉴를 생성하는 UI 컴포넌트입니다. html마크업을 통해서 해당 컴포넌트 기능을 사용할 경우에는 `data-toggle="xe-dropdown"` 속성을 버튼에 사용해 주어야 합니다. 버튼에 해당 속성을 사용해 주게 되면 이벤트가 자동으로 바인딩되어 버튼 기능이 활성화 됩니다.
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
```javascript
//javascript
$('[data-toggle=xe-dropdown]').xeDropdown();
```
### 3. modal
#### $(selector).xeModal( options )
modal창을 생성하는 UI 컴포넌트입니다. html마크업을 통해서 해당 컴포넌트 기능을 사용할 경우에는 `data-toggle="xe-modal"` 속성을 버튼에 사용해 주어야 합니다. 버튼에 해당 속성을 사용해 주게 되면 이벤트가 자동으로 바인딩되어 버튼 기능이 활성화 됩니다.
##### options (object)
* backdrop
* keyboard
* show
* remote


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
```javascript
$('#modal').xeModal();
```
### 4. tooltip
#### $(selector).xeTooltip( options )
tooltip을 생성하는 UI 컴포넌트입니다. html마크업을 통해서 해당 컴포넌트 기능을 사용할 경우에는 `data-toggle="xe-tooltip"` 속성을 버튼에 사용해 주어야 합니다. 버튼에 해당 속성을 사용해 주게 되면 이벤트가 자동으로 바인딩되어 버튼 기능이 활성화 됩니다.
##### options (object)
* animation
* container
* delay
* html
* placement
* selector
* template
* title
* trigger
* viewport


```html
<button type="button" class="xe-btn xe-btn-success" data-toggle="xe-tooltip" data-placement="left" title="Tooltip on left">xe-tooltip on left</button>
```
```javascript
$('[data-toggle="xe-tooltip"]').xeTooltip();
```
### 5. lightbox
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
### 1. dynamicLoadManager
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
### 3. utils
#### Utils.asset( url )
##### url (string)
```javascript
var url = Utils.asset('/asset/test');
console.log(url) //http://localhost:port/asset/test
```