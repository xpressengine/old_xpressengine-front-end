#3.4 Modal
---
## $(selector).xeModal( options )
modal창을 생성하는 UI 컴포넌트입니다. html마크업을 통해서 해당 컴포넌트 기능을 사용할 경우에는 `data-toggle="xe-modal"` 속성을 버튼에 사용해 주어야 합니다. 버튼에 해당 속성을 사용해 주게 되면 이벤트가 자동으로 바인딩되어 버튼 기능이 활성화 됩니다.
### options (object)
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
