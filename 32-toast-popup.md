#3.2 Toast Popup
---

## XE.toast( type, message, pos )
토스트 팝업을 생성하여 메시지를 보여줍니다.
### type (string)
타입은 **danger** | **positive** | **warning** | **success** | **fail** | **error** | **info**로 정의되어 있으며 생성되는 팝업의 스킨을 변경하여 줍니다.
### message (string)
toast popup 생성시 보여줄 메시지를 지정합니다.
### pos (string)
토스트 팝업이 발생하는 위치를 나타내며 지정값으로는 'top', 'topLeft', 'topRight', 'bottom', 'bottomLeft', 'bottomRight'를 사용합니다. 기본값은 'bottom'으로 `pos`파라미터를 사용하지 않을 경우 
화면 하단에서 팝업이 발생합니다.

```javascript
XE.toast('success', '토스트 팝업 생성 성공!');
```

