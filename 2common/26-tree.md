# 2.6 Tree

---
Tree의 기능은 drag & drop을 통한 리스트를 편리하게 구성될 수 있도록 합니다. 기본적으로 jquery ui의 `sortable`과 확장 라이브러리인 `nestedSortable`이 번들링되어 있습니다. 
Tree 기능을 하용하기 위해서 `assets/core/common/js/xe.tree.js`를 로드하여야 합니다.


```php
//blade파일(php)에서 로드할 경우
{{ XeFrontend::js('assets/core/common/js/xe.tree.js')->appendTo('body')->load() }}
```

```html
<-- html에서 로드할 경우 -->
<script type='text/javascript' src='assets/core/common/js/xe-page.js'></script>
```

## Tree.getItemsTemplate(params)
Tree로 구성되는 마크업을 리턴해 줍니다.

### params (object)
* #### rootId (string)
tree의 root id
* #### nodeTemplate (function)
list item 마크업 내에 생성되는 html을 리턴해주는 function
* #### items (object or array)
 * Tree 구성 데이터
 * id - tree node의 id
 * parentId - 상위 node의 id
 * ordering - depth의 정렬 기준
 * items  - 하위 node의 items

## Tree.run($wrap, config, treeOptions)
Tree 기능을 활성화합니다. run메소드를 통해 drag & drop기능이 활성화 되며 활성화시 인자로 받은 config의 메소드들의 기능을 활성화합니다.

### $wrap (jquery object)
tree구성의 wrapper 엘리먼트로 jquery object를 넘겨 받습니다. `(예) $('#wrapper')`

### config (object)
* #### dragStart (function)
drag 시작시 호출
* #### dragStop (function)
drop될 시 호출
* #### update (function)
선택된 노드의 변경사항이 있을 경우 호출. 트리 변경 ajax를 콜백으로 사용하면 됩니다. 인자로 object를 내려주며 선택된 노드, id, parentId, ordering의 정보가 포함되어 있습니다.

```javascript
function update (obj) {
 var $item = obj.item;
 var id = obj.id;
 var parentId = obj.parentId
 var ordering = obj.ordering;
 
 XE.ajax(...)
}
``` 

### treeOptions
이 옵션은 기본적으로는 사용하지 않아도 무관하나 트리의 기능을 추가해야 할 경우 사용합니다.
xe.tree에는 nestedSortable라이브러리가 번들링되어 있습니다. 옵션으로 다양한 기능을 구성할 수 있도록 되어 있으며 treeOptions로 넘겨받은 옵션으로 내부적으로 사용되고 있는 옵션을 추가합니다. 옵션에 대한 자세한 설명은 [링크](https://github.com/mjsarfatti/nestedSortable)를 참조하시면 됩니다.

## Tree.setPrevent(flag)
트리의 이동을 활성화 또는 비활성화 합니다.

#### flag (boolean)
true 또는 false

## Tree.add($container, params, callback)
run메소드를 통한 Tree활성화 이후 Tree에 Node를 추가합니다.

### $container
Node를 추가할 wrapper

### params (object)
* #### items (object)
 * id - tree node의 id
 * parentId - 상위 node의 id
 * ordering - depth의 정렬 기준
 * items  - 하위 node의 items

* #### nested (boolean)
상위 Node가 있을 경우 true, 아니면 false

* #### nodeTemplate (function)
list item 마크업 내에 생성되는 html을 리턴해주는 function

### callback 
노드를 추가한 이후에 호출될 callback