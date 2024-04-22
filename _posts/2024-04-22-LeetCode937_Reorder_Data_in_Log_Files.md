---
title: LeetCode 937. Reorder Data in Log Files
description: Java로 리트코드 937번을 풀기 위해 필요한 메서드를 공부해보자
date: 2024-04-22 23:02:00 +0900
categories: [Algorithm]
tags: [algorithm, java]
author: jooyoon
image: /assets/img/algorithm_preview.png
---

## 문제

  <https://leetcode.com/problems/reorder-data-in-log-files/description/>

  1. 로그의 가장 앞부분은 식별자로서, 순서에 영향을 끼치지 않는다.
  2. 문자로 구성된 로그가 숫자 로그보다 앞에 오며, 문자 로그는 사전순으로 한다.
  3. 문자가 동일할 경우에는 식별자순으로 한다.
  4. 숫자 로그는 입력 순서대로 한다.

## 풀이

  1. 숫자 로그를 담을 List, 문자 로그를 담을 List를 각각 생성한 뒤 담는다.
  2. 문자 로그를 문제에서 주어진 조건에 맞게 정렬한다.
  3. 문자 로그 뒤에 숫자 로그를 이어 붙인다.

## Method 정리

### Collections.sort() VS List.sort()

#### Collections.sort()
  
  -> Collections 클래스의 static method 이다.
  <br>
  -> List를 implement한 클래스를 정렬할 수 있다. (ArrayList, LinkedList 등)
  
  ```java
  Collections.sort(List<T> list);
  Collections.sort(List<T> list, Comparator<? super T> c);
  ```
  ![Java-collections-framework][Java-collections-framework]{:.image-styling}

#### List.sort()
  
  -> List 클래스의 instance method이다.
  -> List의 method이므로 List interface를 implement한 객체에서만 사용할 수 있다.
  
  ```java
  default void sort(Comparator<? super E> c)
  ```
  
  ```java
  import java.util.*;

  public class SortExample {
    public static void main(String[] args) {
      List<Integer> arrayList1 = new ArrayList<>();
      arrayList1.add(3);
      arrayList1.add(1);
      arrayList1.add(2);
        
      List<Integer> arrayList2 = new ArrayList<>();
      arrayList2.add(3);
      arrayList2.add(1);
      arrayList2.add(2);
        
      // Using Collections.sort()
      Collections.sort(arrayList1);
      System.out.println("Using Collections.sort(): " + arrayList1);

      // Using ArrayList.sort()
      arrayList2.sort(null); // Using natural ordering
      System.out.println("Using ArrayList.sort(): " + arrayList2);
    }
  }
  ```

* 두 method 모두 list를 정렬하는데 사용된다.
* Collections.sort()는 Java 1.2에 소개되었고, List.sort()는 Java 8에 소개 되었다.
* Java 8 이후 버전을 쓰고 있다면, 주로 List.sort() 사용이 주로 선호된다.
  <br>
  -> parameter 전달이 필수가 아니기 때문에 overhead 감소로 performance가 더 좋기 때문이다.

### List.toArray()

```java
return letterList.toArray(new String[0]);
```

* List 컨테이너의 인스턴스를 Array로 만들어 주는 것이 toArray()이다. 하지만 parameter가 조금 헷갈린다.
* 간단히 말하자면, List 인스턴스의 크기와 parameter로 들어가는 배열 객체의 크기 중 더 큰 크기로 Array로의 전환이 이루어진다.
* 이 예시에서는 parameter로 들어가는 String 배열의 size가 0이므로, 자연스럽게 letterList의 size로 배열이 만들어 지는 것이다. (String 자료형 Array)
* 공식 문서의 설명은 다음과 같다.
  ![toArray-description][toArray-description]{:.image-styling}
* 문제의 반환값이 String[] 이므로 List를 String Array로 바꾸어 주어야 한다.

### String[] split(String regex, int limit)

* String 클래스의 instance 함수
* Splits this string around matched of the given regular expression → 이후 string array를 반환한다.
* limit → This parameter controls the number of times the pattern is applied and therefore affects the length of the resulting array
  * If ‘limit’ > 0, the pattern will be applied at most ‘limit - 1’ times, and the array’s length will be no greater than ‘limit’.
  ```java
  String text = "Java,spring,backend,java";
  String[] results = text.split(",", 3);
  // results will contain ["java", "spring", "backend,java"]
  // 패턴이 limit - 1 = 2번 적용되고, array의 최대 길이는 3을 넘지 않는다.
  ```
  * If ‘limit’ = 0, the pattern will be applied as many times as possible, and trailing empty strings will be discarded.
  -> 가능한만큼 적용되고, 뒤에 오는 빈 문자열은 삭제된다.
  ```java
  String text = "java:spring:backend:java::";
  String[] results1 = text.split(":", 0);
  // ["java", "spring", "backend", "java"]
  ```
  * If ‘limit’ < 0, the pattern will be applied as many times as possible and the array can have any length.
  -> 마찬가지로 가능한만큼 적용되지만, 뒤에 오는 빈 문자열은 삭제되지 않는다.
  ```java
  String text = "java:spring:backend:java::";
  String[] results2 = text.split(":", -1);
  // ["java", "spring", "backend", "java", "", ""]
  ```
  
[Java-collections-framework]: https://1drv.ms/i/c/bc8220337a33dd52/IQOO_NjWvgxSS5R6WUn3zZYrATE9jH4dKEsKmPZ6ey2NAEg?width=854&height=715
[toArray-description]: https://1drv.ms/i/c/bc8220337a33dd52/IQMLsIYRCST4Rbvy7fnbACt_AWD62S83ShbAI7vkRy0GA3o?width=1201&height=75
