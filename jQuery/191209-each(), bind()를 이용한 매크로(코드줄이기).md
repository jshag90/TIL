**191209-each(), bind()를 이용한 매크로(코드줄이기)**

```javascript
$('#a[href="#xVectorInfoTab"]').click(function(event){
	//이벤트 후 동작들
});

$('#a[href="#yVectorInfoTab"]').click(function(event){
	//이벤트 후 동작들
});

$('#a[href="#pressureInfoTab"]').click(function(event){
	//이벤트 후 동작들
});
```

기존 코드는 유사한 ID값과 동일한 이벤트 동작을 했음

이름 each(), bind() 함수를 통해서 코드줄이기를 함

이름 매크로라고 부름



```javascript
$.each(['xVector', 'yVector', 'pressure'], function(num, tabName){

	$("#a[href='#"+tabName+"InfoTab']").bind('click',function(e){
	  //이벤트 후 공통 동작들
	});

});
```

위와 같이 each와 bind를 이용하여 코드 줄이기를 시도함

기존 레거시 코드를 다음과 같이 매크로와 시키면 좋을 듯함