# 2.2 Form
---

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

## Attributes
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

