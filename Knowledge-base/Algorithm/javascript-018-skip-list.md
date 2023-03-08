---
title: [JavaScript] 018: 건너뛰기 목록
description: 
published: true
date: 2023-02-09T20:32:40.072Z
tags: 
editor: markdown
dateCreated: 2023-02-09T20:32:38.418Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[JavaScript] 018: Skip List***English** document is available*](/en/Knowledge-base/Algorithm/javascript-018-skip-list)
{.links-list}


# 건너뛰기 목록

건너뛰기 목록은 순서가 지정된 요소 시퀀스 내에서 효율적인 검색을 허용하는 데이터 구조입니다. 노드의 계층적 구조를 사용하는 연결 목록 유형으로, 각 노드는 계층 내에서 다른 수준에 있는 다른 노드에 대한 여러 "링크"를 가집니다. 이 건너뛰기 목록은 Pugh가 1990년 논문 "건너뛰기 목록: 균형 트리에 대한 확률적 대안"에서 처음 설명했습니다.

건너뛰기 목록은 무작위 데이터 구조입니다. 즉, 노드가 서로 연결되는 순서는 난수 생성기에 의해 결정됩니다. 이 접근 방식의 장점은 건너뛰기 목록을 O(n) 시간에 구성할 수 있다는 것입니다. 여기서 n은 목록에 삽입할 요소의 수입니다.

건너뛰기 목록에는 데이터베이스 및 파일 시스템을 포함하여 여러 응용 프로그램이 있습니다. Linux 커널의 기수 트리 데이터 구조에서도 사용됩니다.

## 건너뛰기 목록 작동 방식

건너뛰기 목록은 일련의 수준으로 구성되며 각 수준에는 노드 집합이 있습니다. 첫 번째 수준이 가장 낮은 수준이고 마지막 수준이 가장 높은 수준입니다. 레벨 수는 난수 생성기에 의해 결정됩니다.

각 수준의 노드는 정렬된 순서로 함께 연결됩니다. 가장 낮은 수준의 노드는 값이 증가하는 순서로 서로 연결되고 상위 수준의 노드는 값이 감소하는 순서로 서로 연결됩니다.

건너뛰기 목록에는 최하위 수준의 첫 번째 노드인 "헤드" 노드도 있습니다. 헤드 노드에는 다음 레벨의 첫 번째 노드에 대한 포인터가 있습니다. 다음 레벨에 노드가 없으면 헤드 노드의 포인터는 null이 됩니다.

건너뛰기 목록의 각 노드에는 "값" 필드와 "레벨" 필드가 있습니다. value 필드는 노드의 값을 저장하고 level 필드는 노드의 레벨을 저장합니다.

노드의 레벨은 난수 생성기에 의해 결정됩니다. 노드에 레벨 i가 할당될 확률은 1/(2^i)입니다. 즉, 노드가 가장 높은 수준에 할당될 확률은 1/2이고 노드가 두 번째로 높은 수준에 할당될 확률은 1/4입니다.

건너뛰기 목록은 헤드 노드에서 시작하여 같은 수준의 다음 노드에 대한 포인터를 따라 검색됩니다. 다음 노드의 값이 검색 중인 값보다 작으면 포인터는 같은 수준의 다음 노드로 이동합니다. 이 과정은 찾고 있는 값보다 크거나 같은 값을 가진 노드에 도달할 때까지 반복됩니다. 이 시점에서 검색은 포인터를 따라 아래 수준의 다음 노드를 가리키며 프로세스를 반복합니다.

검색 중인 값이 건너뛰기 목록에 없으면 검색 결과 null이 반환됩니다.

## 코드 예

다음은 건너뛰기 목록의 간단한 Java 구현입니다. "SkipList" 클래스는 건너뛰기 목록을 나타내고 "Node" 클래스는 건너뛰기 목록의 노드를 나타냅니다.

```java
public class SkipList {
    
    private Node head;
    private int size;
    private Random random;
    
    public SkipList() {
        head = new Node(Integer.MIN_VALUE);
        size = 0;
        random = new Random();
    }
    
    public void insert(int value) {
        Node node = new Node(value);
        Node current = head;
        while (current.value < value) {
            current = current.next;
        }
        node.next = current.next;
        current.next = node;
        size++;
    }
    
    public boolean contains(int value) {
        Node current = head;
        while (current.value < value) {
            current = current.next;
        }
        return current.value == value;
    }
    
    public int size() {
        return size;
    }
    
    private class Node {
        int value;
        Node next;
        
        public Node(int value) {
            this.value = value;
        }
    }
    
}
```

## 운동

1. SkipList 클래스에 대한 "insert" 및 "contains" 메소드를 구현합니다.

2. 단일 연결 목록 대신 이중 연결 목록을 사용하도록 SkipList 클래스를 수정합니다.

3. SkipList 클래스를 수정하여 각 수준에서 노드 수를 추적합니다.

4. SkipList 클래스를 수정하여 목록의 요소 순서를 지정하는 데 사용자 지정 비교기를 사용할 수 있습니다.

5. SkipList 클래스를 수정하여 목록의 요소를 해시하는 데 사용자 지정 해시 함수를 사용할 수 있도록 합니다.