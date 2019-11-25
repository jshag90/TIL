``StringTokenizer``

Java에서 string을 token단위로 끊어 주는 StringTokenizer클래스를 제공함

`` StringTokenizer(String str)``

```java
String str = "a b c";
StringTokenizer tokenizer = new StringTokenizer(str);
System.out.println(tokenizer.countTokens()); // 3

while(tokenizer.hasMoreTokens()){
		System.out.println(tokenizer.nextToken());
}
```

결과값

```
3
a
b
c
```

``StringTokenizer(String str, String delim)``

```java
String str = "a%b%c";
StringTokenizer tokenizer = new StringTokenizer(str,"%");
System.out.println(tokenizer.countTokens());
		
while(tokenizer.hasMoreTokens()){
    System.out.println(tokenizer.nextToken());
}
```

결과값

```
3
a
b
c
```

``StringTokenizer(String str, String delilm, boolean returnDelims)``

returnDelims가 true이면 구획문자를 리턴하게됨

```java
String str = "a%b%c";
StringTokenizer tokenizer = new StringTokenizer(str,"%",true);
System.out.println(tokenizer.countTokens());

while(tokenizer.hasMoreTokens()){
    System.out.println(tokenizer.nextToken());
}
```

결과값

```
5
a
%
b
%
c
```

