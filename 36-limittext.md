#3.6 LimitText
---
input요소에 text값의 Size 및 Byte를 제한하는 컴포넌트 입니다. 
이 기능을 사용하기 위해서는 xe-limitText.js 파일을 로드하여야 합니다.

```php
//blade파일(php)에서 로드할 경우
{{ XeFrontend::js('assets/core/xe-ui-component/js/xe-limitText.js')->appendTo('body')->load() }}

```
```html
<-- html에서 로드할 경우 -->
<script type='text/javascript' src='assets/core/xe-ui-component/js/xe-limitText.js'></script>
```

## $(selector).limitText( options )
### options (Object)

| 옵션명        | type   | 내용 |
|-------------|:------:|------|
| limit       | Number | 입력 제한 count 또는 byte, default 30     |
| limitBy     | String | 'count' 또는 'byte' 입력 제한 요소     |
| showLimitBox| Boolean | count박스를 보여줄지의 여부     |
| position    | String | 'inner' 또는 'outer', count박스 위치가 input요소 내부 또는 외부에 위치됨    |
| onOverCount | Function | 입력 제한 카운트의 범위를 초과하여 입력될 경우 실행될 callback     |
| onKeyup     | Function | keyup이 될경우 호출될 callback     |
| onKeydown   | Function | keydown이 될경우 호출될 callback     |





