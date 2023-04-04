---
title: Java에서 null 체크하는 방법: variable == null vs Objects.isNull()
description: 
published: true
date: 2023-04-04T02:46:58.657Z
tags: java
editor: markdown
dateCreated: 2023-04-04T02:44:38.925Z
---


![java-logo.png](/java-logo.png){.align-center}

Java 언어에서 null 체크를 수행하는 방법 중 하나는 `variable == null`과 같이 변수와 `null`을 직접 비교하는 것입니다. 그러나 Java 7 이후에 도입된 `Objects.isNull()` 메소드를 사용하여 null 체크를 수행하는 것도 가능합니다.

## Objects.isNull() 메소드

```java
    /**
     * Returns {@code true} if the provided reference is {@code null} otherwise
     * returns {@code false}.
     *
     * @apiNote This method exists to be used as a
     * {@link java.util.function.Predicate}, {@code filter(Objects::isNull)}
     *
     * @param obj a reference to be checked against {@code null}
     * @return {@code true} if the provided reference is {@code null} otherwise
     * {@code false}
     *
     * @see java.util.function.Predicate
     * @since 1.8
     */
    public static boolean isNull(Object obj) {
        return obj == null;
    }

```

`Objects.isNull()` 메소드는 주어진 객체가 null인지 아닌지를 검사하여 `boolean` 값을 반환하는 일반적인 유틸리티 메소드입니다. 이 메소드는 Java 함수형 프로그래밍의 핵심 개념 중 하나인 함수형 인터페이스에 적합하다는 것을 의미하여, `java.util.function.Predicate`에서도 사용될 수 있습니다.

## Objects.isNull() 메소드의 if문에서의 사용에 관한 논란

`Objects.isNull()` 메소드가 `java.util.function.Predicate`에서 사용될 수 있다는 것을 강조하는 주석 때문에, `if`문에서 `Objects.isNull()`을 사용하는 것은 최초 개발 당시의 의도에 반하는 코드 작성이라는 의견이 있습니다. 또한, 메소드 호출이 추가되는 것이 미세한 성능 차이를 일으킬 수 있기 때문에, `variable == null`와 같이 변수와 `null`을 직접 비교하는 것이 성능면에서 더 효율적이라는 의견도 있습니다.

## 논란 해결책

**`Objects.isNull()` 메소드가 `Predicate`에서 사용될 수 있다는 것은 이 메소드가 함수형 프로그래밍에서 중요한 역할을 수행한다는 것을 보여줍니다. 이러한 특성은 `if`문에서도 `Objects.isNull()`을 사용할 수 있음을 시사합니다. `Objects.isNull()` 메소드는 null 체크를 위한 일반적인 유틸리티 메소드이기 때문에, `if`문에서도 null 체크를 수행하는데 사용될 수 있습니다.**

성능 문제가 발생할 가능성이 있는 경우에는 `variable == null`과 같이 변수와 `null`을 직접 비교하는 것이 더 적절할 수 있습니다. 이는 메소드 호출을 최소화하는 것이 목적이므로, null 체크가 빈번하게 일어나는 경우에는 성능상 이점이 있을 수 있습니다.

따라서, 이러한 논란을 해결하기 위해서는 상황에 맞는 방법으로 null 체크를 수행하는 것이 중요합니다. 일관된 방식으로 null 체크를 수행하고, 코드의 가독성과 유지보수성을 고려하여 `Objects.isNull()`을 사용하는 것이 좋습니다. 그리고, 성능 문제가 발생할 가능성이 있는 경우에는 `variable == null`과 같이 변수와 `null`을 직접 비교하는 것이 더 적절할 수 있습니다.

## 결론

Java에서 null 체크를 수행하는 방법으로는 `variable == null`과 `Objects.isNull()`이 있습니다. 이 중에서도 상황에 따라 적절한 방법을 선택하여 사용하는 것이 중요합니다. **`Objects.isNull()` 메소드는 null 체크를 위한 일반적인 유틸리티 메소드이며, `Predicate`에서 사용될 수 있다는 점은 `if`문에서 이 메소드를 사용하는 것이 잘못된 것이 아니라는 것을 보여줍니다.** 따라서, 이러한 논란을 해결하기 위해서는 일관된 방식으로 null 체크를 수행하고, 코드의 가독성과 유지보수성을 고려하여 `Objects.isNull()`을 사용하는 것이 좋습니다. 그리고, 성능 문제가 발생할 가능성이 있는 경우에는 `variable == null`과 같이 변수와 `null`을 직접 비교하는 것이 더 적절할 수 있습니다.

개발자들은 이러한 논란을 고려하여 상황과 프로젝트 요구 사항에 맞게 Java에서 null 체크를 수행하는 방법을 선택해야 합니다. 일반적으로, 가독성과 코드의 유지보수성이 중요한 경우에는 `Objects.isNull()` 메소드를 사용하고, 성능이 중요한 경우에는 `variable == null`과 같이 변수와 `null`을 직접 비교하는 방법을 사용할 수 있습니다. 이렇게 상황에 맞는 방법을 선택하면 코드의 품질과 성능을 모두 만족할 수 있습니다.

