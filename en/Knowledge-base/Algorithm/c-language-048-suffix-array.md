---
title: [C Language] 048: Suffix Array
description: 
published: true
date: 2023-02-10T15:17:52.387Z
tags: 
editor: markdown
dateCreated: 2023-02-10T15:17:46.042Z
---

- [[Lenguaje C] 048: matriz de sufijos***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-048-suffix-array)
{.links-list}
- [[C语言]048：后缀数组***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-048-suffix-array)
{.links-list}
- [[ C 언어 ] 048 : 접미사 배열***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-048-suffix-array)
{.links-list}


# 048: Suffix Array

The suffix array is a fundamental data structure used in text processing and string matching algorithms. It is an array of all the suffixes of a given string, sorted in lexicographical order.

The suffix array can be used to efficiently find all occurrences of a given pattern in a string, as well as to find the longest common substring of two strings.

## Theory

A suffix array is a sorted array of all the suffixes of a given string. The suffixes are sorted in lexicographical order.

The suffix array can be used to efficiently find all occurrences of a given pattern in a string, as well as to find the longest common substring of two strings.

The suffix array can be constructed in O(n log n) time using the Suffix Sort algorithm.

## Code Examples

### Constructing a Suffix Array

The following code example shows how to construct a suffix array in Java using the Suffix Sort algorithm.

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

### Finding All Occurrences of a Pattern

The following code example shows how to use the suffix array to find all occurrences of a given pattern in a string.

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

### Finding the Longest Common Substring

The following code example shows how to use the suffix array to find the longest common substring of two strings.

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

## Exercises

1. Implement the Suffix Sort algorithm in your chosen programming language.

2. Use the suffix array to find all occurrences of a given pattern in a string.

3. Use the suffix array to find the longest common substring of two strings.