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
### options
#### - limit
#### - limitBy
#### - showLimitBox
#### - position
#### - onOverCount
#### - onKeyup
#### - onKeydown


