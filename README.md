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

## [Your order, please](https://www.codewars.com/kata/55c45be3b2079eccff00010f/java)

Your task is to sort a given string. Each word in the string will contain a single number.
This number is the position the word should have in the result.

Note: Numbers can be from 1 to 9. So 1 will be the first word (not 0).

If the input string is empty, return an empty string.
The words in the input String will only contain valid consecutive numbers.
 
```java
"is2 Thi1s T4est 3a"  -->  "Thi1s is2 3a T4est"
"4of Fo1r pe6ople g3ood th5e the2"  -->  "Fo1r the2 g3ood 4of th5e pe6ople"
""  -->  ""
```

### Solution
Nasty.
```java
import java.util.stream.Collectors;
import java.util.Arrays;

public class Order {
    public static String order(String words) {
        String[] strings = words.split(" ");
        return Arrays.stream(strings).sorted(
                (String x, String y) -> (
                        x.chars().filter((t) -> Character.isDigit((char)(t))).findAny().getAsInt()
                                - y.chars().filter((t) -> Character.isDigit((char)(t))).findAny().getAsInt()
                )
        ).collect(Collectors.joining(" "));
    }
}
```

### Featured solution
An elegant one.
```java
import java.util.Arrays;
import java.util.Comparator;

public class Order {
    public static String order(String words) {
        return Arrays.stream(words.split(" "))
                .sorted(Comparator.comparing(s -> Integer.valueOf(s.replaceAll("\\D", ""))))
                .reduce((a, b) -> a + " " + b).get();
    }
}
```

## [Valid Braces](https://www.codewars.com/kata/5277c8a221e209d3f6000b56/java)

Write a function that takes a string of braces, and determines if the order of the braces is valid. It should return true if the string is valid, and false if it's invalid.

This Kata is similar to the Valid Parentheses Kata, but introduces new characters: brackets [], and curly braces {}. Thanks to @arnedag for the idea!

All input strings will be nonempty, and will only consist of parentheses, brackets and curly braces: ()[]{}.

What is considered Valid?
A string of braces is considered valid if all braces are matched with the correct brace.
 
```java
"(){}[]"   =>  True
"([{}])"   =>  True
"(}"       =>  False
"[(])"     =>  False
"[({})](]" =>  False
```

### Solution
```java
import java.util.Stack;

public class BraceChecker {

    public boolean isValid(String braces) {
        Stack<Character> container = new Stack<Character>();

        for (char c : braces.toCharArray()) {

            if (c == ' ') {
                continue;
            }

            if (c == '(' || c == '{' || c == '[') {
                container.push(c);
            } else if (c == ')' && !container.isEmpty() && container.peek() == '('
                    || (c == '}' && !container.isEmpty() && container.peek() == '{')
                    || (c == ']' && !container.isEmpty() && container.peek() == '[')) {
                container.pop();
            } else {
                return false;
            }

        }

        return container.isEmpty();
    }

}
```

### Featured solution
An elegant one.
```java
import java.util.Stack;

public class BraceChecker {

    public boolean isValid(String braces) {
        Stack<Character> s = new Stack<>();
        for (char c : braces.toCharArray())
            if (s.size() > 0 && isClosing(s.peek(), c)) s.pop();
            else s.push(c);
        return s.size() == 0;
    }

    public boolean isClosing(char x, char c) {
        return (x == '{' && c == '}') || (x == '(' && c == ')') || (x == '[' && c == ']');
    }

}
```



## [Number of trailing zeros of N!](https://www.codewars.com/kata/52f787eb172a8b4ae1000a34/java)

Write a program that will calculate the
number of trailing zeros in a factorial of a given number.

```java
zeros(6) = 1
# 6! = 1 * 2 * 3 * 4 * 5 * 6 = 720 --> 1 trailing zero

zeros(12) = 2
# 12! = 479001600 --> 2 trailing zeros
```

### Solution
```java
public class Solution {
    public static int zeros(int n) {
        if (n < 0)
            return -1;

        int count = 0;

        for (int i = 5; n / i >= 1; i *= 5)
            count += n / i;

        return count;
    }
}
```

### Featured solution
```java
public class Solution {
    public static int zeros(int n) {
        if(n/5 == 0)
            return 0;
        return n/5 + zeros(n/5);
    }
}
```

