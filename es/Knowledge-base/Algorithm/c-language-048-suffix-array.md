---
title: [Lenguaje C] 048: matriz de sufijos
description: 
published: true
date: 2023-02-10T15:17:47.662Z
tags: 
editor: markdown
dateCreated: 2023-02-10T15:17:46.038Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 048: Suffix Array***English** document is available*](/en/Knowledge-base/Algorithm/c-language-048-suffix-array)
{.links-list}


# 048: matriz de sufijos

La matriz de sufijos es una estructura de datos fundamental utilizada en el procesamiento de texto y algoritmos de coincidencia de cadenas. Es una matriz de todos los sufijos de una cadena determinada, ordenados en orden lexicográfico.

La matriz de sufijos se puede usar para encontrar de manera eficiente todas las ocurrencias de un patrón dado en una cadena, así como para encontrar la subcadena común más larga de dos cadenas.

## Teoría

Una matriz de sufijos es una matriz ordenada de todos los sufijos de una cadena dada. Los sufijos están ordenados en orden lexicográfico.

La matriz de sufijos se puede usar para encontrar de manera eficiente todas las ocurrencias de un patrón dado en una cadena, así como para encontrar la subcadena común más larga de dos cadenas.

La matriz de sufijos se puede construir en tiempo O (n log n) utilizando el algoritmo de clasificación de sufijos.

## Ejemplos de código

### Construcción de una matriz de sufijos

El siguiente ejemplo de código muestra cómo construir una matriz de sufijos en Java utilizando el algoritmo Suffix Sort.

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

### Encontrar todas las ocurrencias de un patrón

El siguiente ejemplo de código muestra cómo usar la matriz de sufijos para encontrar todas las apariciones de un patrón determinado en una cadena.

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

### Encontrar la subcadena común más larga

El siguiente ejemplo de código muestra cómo usar la matriz de sufijos para encontrar la subcadena común más larga de dos cadenas.

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

## Ejercicios

1. Implemente el algoritmo Suffix Sort en su lenguaje de programación elegido.

2. Use la matriz de sufijos para encontrar todas las ocurrencias de un patrón dado en una cadena.

3. Use la matriz de sufijos para encontrar la subcadena común más larga de dos cadenas.