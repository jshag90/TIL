``StringTokenizer``

Java에서 string을 token단위로 끊어 주는 StringTokenizer클래스를 제공함

```java
String str = "a b c";
StringTokenizer tokenizer = new StringTokenizer(str);
System.out.println(tokenizer.countTokens()); // 3

while(tokenizer.hasMoreTokens()){
		System.out.println(tokenizer.nextToken());
}
```



