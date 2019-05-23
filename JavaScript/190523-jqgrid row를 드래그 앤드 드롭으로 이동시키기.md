**jqgrid row를 드래그 앤드 드롭으로 이동시키기**

```javascript
$('[jqgrid id]').jqGrid('sortableRows',{
	update : function( e, html){ // 순서가 바뀌면 발생되는 event
		console.log( html.item[0].id ); // row id 확인
	}
});
```

