**가상환경 OS에서 SecureRandom 사용시 톰캣 지연 로딩 문제**

java api 중에서 SecureRandom은 기본 적으로 랜덤값을 생성할때 CPU온도 및 하드웨어 정보를 가지고

엔트로피값을 생성한다고 합니다. 

그래서 가상환경에서 톰캣이 기본 옵션일 경우 java의 heap이 꽉차게 되어서 톰캣이 느려지는 경우가 발생한다.

가상환경의 경우에는 톰캣 옵션으로 하드웨어 정보를 가지고 엔드로피를 생성하지 못하도록 설정합니다.

1) 톰캣 설치 경로 이동

2) bin/catalina.sh 파일 수정

3) 다음 부분으로 이동

```java
JAVA_OPTS="$JAVA_OPTS$JSSE_OPTS"
```

4) 다음과 같이 수정

```java
JAVA_OPTS="$JAVA_OPTS$JSSE_OPTS-Djava.security.egd=file:/dev/./urandom"
```



