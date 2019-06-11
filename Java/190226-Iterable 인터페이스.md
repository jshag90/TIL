**Iterable 인터페이스**

- 자바의 컬렉션 최상위 인터페이스이다.  

- Collection이 Iterable이라는 인터페이스를 implements하고 있다. 

- 하위로 Collection을 List, Set, Queue 등이 implements하고 있다. 

- Iterable 인터페이스는 내부에 Iterator 인터페이스를 리턴하는 메소드를 정의하고 있다. 

- Iterator는 컬렉션에 저장되어 있는 요소들을 읽어오는 방법을 표준화 하였는데 그 중 하나가 Iterator이다.

- ```java
  public interface Iterator{
      boolean hasNext();
      Object next();
      void remove();
  }
  ```

  

- 우리가 실제로 사용하는 Iterator it = list.iterator() 는 어떤 List/Set의 구현 클래스인지에 따라 Iterator의 메소드도 달라지는 것이다.

```java
public class ExampleIterable<T> implements Iterable<T>{
    
    public Iterator<T> iterator(){
        return null;
    }
    
}
```



