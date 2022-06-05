# java_tasks

Репозиторий для решения задач по Java

## [List Filtering](https://www.codewars.com/kata/53dbd5315a3c69eed20002dd/java)

In this kata you will create a function that takes a list of non-negative integers and strings and returns a new list
with the strings filtered out.

```java
Kata.filterList(List.of(1,2,"a","b"))=>List.of(1,2)
Kata.filterList(List.of(1,2,"a","b",0,15))=>List.of(1,2,0,15)
Kata.filterList(List.of(1,2,"a","b","aasf","1","123",231))=>List.of(1,2,231)
```

### Solution
```java
import java.util.List;

public class Kata {
  
  public static List<Object> filterList(final List<Object> list) {
    return list.stream()
            .filter((x) -> x.getClass() == Integer.class && (Integer)x >= 0)
            .toList();
  }
}

```
### Featured solution
```java
import java.util.*;
import java.util.stream.Collectors;

public class Kata {
  
  public static List filterList(final List<Object> list) {
    return list.stream()
      .filter(e -> e instanceof Integer)
      .collect(Collectors.toList());
  }

}
```