# 2.3 Form Validator
---

Form Validator를 사용하기 위해서는 **validator.js**파일을 로드하여야 합니다.

```php
//blade파일(php)에서 로드할 경우
{{ XeFrontend::js('assets/core/common/js/validator.js')->appendTo('body')->load() }}

```
```html
<-- html에서 로드할 경우 -->
<script type='text/javascript' src='assets/core/common/js/validator.js'></script>
```

## XE.formValidate( $form )
해당 폼 요소에 있는 값들의 유효성을 체크합니다. 마크업에 있는 element의 data-valid attribute에 정의된 유효성을 체크합니다. 유효성 체크를 하고자 하는 내용을 '|'구분하여 지정하면 여러개의 유효성을 체크하게되고 유효성이 통과하지 못할 경우 메시지를 노출합니다.

## Attribute
### 1. data-rule-alert-type
유효성 체크를 통과하지 못할 경우 보여질 메시지형태를 정의합니다. 메시지형태는 toast, form 2가지 요소가 있습니다.
* toast
  - XE.toast 팝업의 형태로 메시지가 노출됩니다.
* form
  - 해당 필드 요소하단에 메시지가 노출됩니다.
  
```html
<form data-rule-alert-type="toast"> <!-- toast or form -->
...
</form>
```

### 2. data-valid
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

