# 1.1 XE.Lang

## XE.Lang.trans( id [, parameter] )
설정되어 있는 언어에 등록되어 있는 다국어를 리턴해줍니다.
### id (string)
다국어가 정의된 key값을 지정합니다. ( 필수 요소 )
### parameter (object)
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

