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
* alphanum 또는 alpha_num
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
* accepted
 - 필드의 값이 yes, on, 1, 또는 _true_이어야 합니다.
* alpha_dash
 - 필드의 값이 (숫자나 기호가 아닌) 알파벳[자음과 모음] 문자 및 숫자와 dash(-), underscore(_)로 이루어져야 합니다.
* array
 - 필드의 값이 배열형태이어야 합니다.
* boolean
 - 필드의 값이 반드시 true, false, 1, 0, "1", "0" 이어야 합니다.
* date
 - 필드의 값이 strtotime PHP 함수에서 인식할 수 있는 올바른 날짜여야 합니다.
* date_format:format
 - 필드의 값이 반드시 주어진 format과 일지해야 합니다.
* digits:value
 - 필드의 값이 반드시 숫자여야 하고, 길이가 value이어야 합니다
* digits_between:min,max
 - 필드의 값이 주어진 min과 max사이의 길이를 가져야 합니다.
* filled
 - 필드가 존재하는 경우 값이 비어있으면 안됩니다.
* integer
 - 필드의 값이 정수여야 합니다.
* ip
 - 필드의 값이 IP 주소여야 합니다.
* ipv4
 - 필드의 값이 IPv4 주소여야 합니다.
* ipv6
 - 필드의 값이 IPv6 주소여야 합니다.
* mimes:foo,bar...
 - 파일의 MIME 타입이 주어진 확장자 리스트 중에 하나와 일치해야 합니다.
* nullable
 - 필드의 값은 null 일 수 있습니다. 
* regex:pattern
 - 필드의 값이 주어진 정규식 표현과 일치해야 합니다.
* json
 - 필드의 값이 유효한 JSON 문자열이어야 합니다.
* string
 - 필드의 값이 반드시 문자열이어야 합니다.

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

