**자바스트립트 특정 문자 바꾸기**

1) String prototype 메서드 추가

```
//replaceAll prototype 선언
String.prototype.replaceAll = function(org, dest) {
    return this.split(org).join(dest);
}
```

var str="aac";

str = str.replaceAll("c","a");



2) 정규식 사용

var str ="aac";

str = str.replace(/c/g,"a");



http://gent.tistory.com/18

