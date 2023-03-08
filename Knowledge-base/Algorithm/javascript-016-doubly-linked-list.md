---
title: [JavaScript] 016: 이중 연결 목록
description: 
published: true
date: 2023-02-09T18:32:31.927Z
tags: 
editor: markdown
dateCreated: 2023-02-09T18:32:30.291Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[JavaScript] 016: Doubly Linked List***English** document is available*](/en/Knowledge-base/Algorithm/javascript-016-doubly-linked-list)
{.links-list}


# JavaScript 016: 이중 연결 목록

이중 연결 리스트는 각 노드가 이전 노드와 다음 노드에 대한 참조를 포함하는 방식으로 함께 연결된 일련의 순차 노드로 구성된 데이터 구조입니다. 이 유형의 연결 목록은 양방향 순회가 가능하기 때문에 단일 연결 목록보다 유리합니다.

일반적인 이중 연결 목록 노드에는 세 개의 필드가 있습니다.

- **prev**: 목록의 이전 노드에 대한 참조
- **다음**: 목록의 다음 노드에 대한 참조
- **데이터**: 노드에 저장된 데이터

이중 연결 목록의 첫 번째 노드는 일반적으로 **head** 노드라고 하며 마지막 노드는 일반적으로 **tail** 노드라고 합니다. 헤드 노드와 테일 노드는 헤드 노드의 prev 필드가 null이고 테일 노드의 next 필드가 null이라는 특별한 속성을 가지고 있습니다.

다음은 4개의 노드가 있는 이중 연결 목록의 그림입니다.

![이중 연결 목록](https://i.imgur.com/eLzWqlN.png)

다음은 JavaScript의 기본 이중 연결 목록 노드에 대한 코드입니다.

```javascript
function Node(data) {
  this.prev = null;
  this.next = null;
  this.data = data;
}
```

이중 연결 리스트에 새 노드를 삽입하려면 먼저 새 노드를 삽입하려는 노드를 찾아야 합니다. 해당 노드를 찾으면 찾은 노드를 가리키도록 새 노드의 next 필드를 설정할 수 있고 새 노드를 가리키도록 찾은 노드의 prev 필드를 설정할 수 있습니다. 마지막으로 찾은 노드를 가리키도록 새 노드의 prev 필드를 설정할 수 있습니다.

다음은 이 삽입 프로세스의 모습을 보여 주는 그림입니다.

![이중 연결 목록에 삽입](https://i.imgur.com/TGiukgD.png)

다음은 이 삽입 프로세스에 대한 코드입니다.

```javascript
function insertAfter(node, newNode) {
  newNode.next = node.next;
  node.next = newNode;
  newNode.prev = node;
}
```

이중 연결 리스트에서 노드를 삭제하려면 먼저 삭제할 노드를 찾아야 합니다. 노드를 찾으면 노드의 next 필드의 prev 필드가 노드의 prev 필드를 가리키도록 설정할 수 있고 노드의 prev 필드의 next 필드가 노드의 next 필드를 가리키도록 설정할 수 있습니다. 마지막으로 노드의 prev 필드와 next 필드를 null로 설정할 수 있습니다.

다음은 이 삭제 프로세스의 모습을 보여 주는 그림입니다.

![이중 연결 목록에서 삭제](https://i.imgur.com/FgxLbNv.png)

다음은 이 삭제 프로세스에 대한 코드입니다.

```javascript
function deleteNode(node) {
  node.prev.next = node.next;
  node.next.prev = node.prev;
  node.prev = null;
  node.next = null;
}
```

그게 전부입니다! 이중 연결 목록은 다양한 응용 프로그램에서 사용할 수 있는 단순하면서도 강력한 데이터 구조입니다.