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
                .filter((x) -> x.getClass() == Integer.class && (Integer) x >= 0)
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

## [Sum of Digits / Digital Root](https://www.codewars.com/kata/541c8630095125aba6000c00/java)

Given n, take the sum of the digits of n. If that value has more than one digit, continue reducing in this way until a
single-digit number is produced. The input will be a non-negative integer.

### Solution

```java
public class DRoot {
    public static int digital_root(int n) {
        return n == 0 ? 0 : 1 + (n - 1) % 9;
    }
}
```

### Featured solution

```java
public class DRoot {
    public static int digital_root(int n) {
        return (n != 0 && n % 9 == 0) ? 9 : n % 9;
    }
}
```

## [Detect Pangram](https://www.codewars.com/kata/545cedaa9943f7fe7b000048/java)

A pangram is a sentence that contains every single letter of the alphabet at least once.
For example, the sentence "The quick brown fox jumps over the lazy dog" is a pangram,
because it uses the letters A-Z at least once (case is irrelevant).

Given a string, detect whether or not it is a pangram.
Return True if it is, False if not. Ignore numbers and punctuation.

### Solution
 I might have written a better one 😉
```java
import java.util.HashSet;

public class PangramChecker {
    public boolean check(String sentence) {
        HashSet<Character> letters = new HashSet<>();
        for (char l : sentence.toCharArray()) {
            if (Character.isLetter(l))
                letters.add(Character.toLowerCase(l));

        }
        return letters.size() == 26;
    }
}
```

### Featured solution

```java
class PangramChecker {
    boolean check(final String sentence) {
        return sentence.chars()
                .filter(Character::isLetter)
                .map(Character::toLowerCase)
                .distinct()
                .count() == 26;
    }
}
```