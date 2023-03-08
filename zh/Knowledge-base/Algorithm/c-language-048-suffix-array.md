---
title: [C语言]048：后缀数组
description: 
published: true
date: 2023-02-10T15:17:47.663Z
tags: 
editor: markdown
dateCreated: 2023-02-10T15:17:46.039Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 048: Suffix Array***English** document is available*](/en/Knowledge-base/Algorithm/c-language-048-suffix-array)
{.links-list}


# 048：后缀数组

后缀数组是文本处理和字符串匹配算法中使用的基本数据结构。它是给定字符串的所有后缀的数组，按字典顺序排序。

后缀数组可用于有效地查找字符串中给定模式的所有出现，以及查找两个字符串的最长公共子串。

## 理论

后缀数组是给定字符串的所有后缀的排序数组。后缀按字典顺序排序。

后缀数组可用于有效地查找字符串中给定模式的所有出现，以及查找两个字符串的最长公共子串。

使用后缀排序算法可以在 O(n log n) 时间内构造后缀数组。

## 代码示例

### 构造后缀数组

以下代码示例显示如何使用后缀排序算法在 Java 中构造后缀数组。

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

### 查找所有出现的模式

下面的代码示例演示如何使用后缀数组查找字符串中给定模式的所有匹配项。

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

### 寻找最长公共子串

下面的代码示例显示了如何使用后缀数组查找两个字符串的最长公共子串。

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

## 练习

1. 用你选择的编程语言实现后缀排序算法。

2. 使用后缀数组查找字符串中给定模式的所有出现。

3、利用后缀数组求两个字符串的最长公共子串。