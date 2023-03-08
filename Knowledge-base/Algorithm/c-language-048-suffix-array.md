---
title: [ C 언어 ] 048 : 접미사 배열
description: 
published: true
date: 2023-02-10T15:17:47.685Z
tags: 
editor: markdown
dateCreated: 2023-02-10T15:17:46.035Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[C Language] 048: Suffix Array***English** document is available*](/en/Knowledge-base/Algorithm/c-language-048-suffix-array)
{.links-list}


# 048: 접미사 배열

접미사 배열은 텍스트 처리 및 문자열 일치 알고리즘에 사용되는 기본 데이터 구조입니다. 사전순으로 정렬된 주어진 문자열의 모든 접미사 배열입니다.

접미사 배열은 문자열에서 주어진 패턴의 모든 항목을 효율적으로 찾고 두 문자열의 가장 긴 공통 하위 문자열을 찾는 데 사용할 수 있습니다.

## 이론

접미사 배열은 주어진 문자열의 모든 접미사의 정렬된 배열입니다. 접미사는 사전순으로 정렬됩니다.

접미사 배열은 문자열에서 주어진 패턴의 모든 항목을 효율적으로 찾고 두 문자열의 가장 긴 공통 하위 문자열을 찾는 데 사용할 수 있습니다.

접미사 배열은 접미사 정렬 알고리즘을 사용하여 O(n log n) 시간으로 구성할 수 있습니다.

## 코드 예제

### 접미사 배열 구성

다음 코드 예제는 접미사 정렬 알고리즘을 사용하여 Java에서 접미사 배열을 구성하는 방법을 보여줍니다.

```java
public static int[] suffixArray(String s) {
  int n = s.length();
  int[] suffixes = new int[n];
  
  for (int i = 0; i < n; i++) {
    suffixes[i] = i;
  }
  
  Arrays.sort(suffixes, (a, b) -> s.substring(a).compareTo(s.substring(b)));
  
  return suffixes;
}
```

### 패턴의 모든 항목 찾기

다음 코드 예제에서는 접미사 배열을 사용하여 문자열에서 지정된 패턴의 모든 항목을 찾는 방법을 보여줍니다.

```java
public static List<Integer> findOccurrences(String s, String pattern) {
  int n = s.length();
  int m = pattern.length();
  
  int[] suffixes = suffixArray(s);
  int l = 0;
  int r = n - 1;
  
  while (l <= r) {
    int mid = l + (r - l) / 2;
    int res = s.substring(suffixes[mid]).compareTo(pattern);
    
    if (res == 0) {
      // Found a match!
      // Now, we need to find the first and last occurrences
      // of the pattern in the suffix array.
      int first = mid;
      int last = mid;
      
      while (first > 0 && s.substring(suffixes[first - 1]).compareTo(pattern) == 0) {
        first--;
      }
      
      while (last < n - 1 && s.substring(suffixes[last + 1]).compareTo(pattern) == 0) {
        last++;
      }
      
      // Now, we have the first and last occurrences of the pattern.
      // We can return all the occurrences in the range [first, last].
      List<Integer> occurrences = new ArrayList<>();
      
      for (int i = first; i <= last; i++) {
        occurrences.add(suffixes[i]);
      }
      
      return occurrences;
    } else if (res < 0) {
      l = mid + 1;
    } else {
      r = mid - 1;
    }
  }
  
  // Pattern not found
  return Collections.emptyList();
}
```

### 가장 긴 공통 하위 문자열 찾기

다음 코드 예제에서는 접미사 배열을 사용하여 두 문자열의 가장 긴 공통 하위 문자열을 찾는 방법을 보여줍니다.

```java
public static String longestCommonSubstring(String s1, String s2) {
  int n1 = s1.length();
  int n2 = s2.length();
  
  int[] suffixes1 = suffixArray(s1);
  int[] suffixes2 = suffixArray(s2);
  
  int l = 0;
  int r = Math.min(n1, n2) - 1;
  String longestCommonSubstring = "";
  
  while (l <= r) {
    int mid = l + (r - l) / 2;
    String substring1 = s1.substring(suffixes1[mid]);
    String substring2 = s2.substring(suffixes2[mid]);
    int len = commonPrefix(substring1, substring2);
    
    if (len > longestCommonSubstring.length()) {
      longestCommonSubstring = substring1.substring(0, len);
    }
    
    if (substring1.compareTo(substring2) < 0) {
      l = mid + 1;
    } else {
      r = mid - 1;
    }
  }
  
  return longestCommonSubstring;
}

private static int commonPrefix(String s1, String s2) {
  int n = Math.min(s1.length(), s2.length());
  
  for (int i = 0; i < n; i++) {
    if (s1.charAt(i) != s2.charAt(i)) {
      return i;
    }
  }
  
  return n;
}
```

## 운동

1. 선택한 프로그래밍 언어로 접미사 정렬 알고리즘을 구현합니다.

2. 접미사 배열을 사용하여 문자열에서 주어진 패턴의 모든 항목을 찾습니다.

3. 접미사 배열을 사용하여 두 문자열의 가장 긴 공통 하위 문자열을 찾습니다.