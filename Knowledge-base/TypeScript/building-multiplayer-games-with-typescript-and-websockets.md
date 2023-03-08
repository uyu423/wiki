---
title: TypeScript 및 WebSocket으로 멀티플레이어 게임 구축
description: 
published: true
date: 2023-02-27T12:33:43.144Z
tags: 
editor: markdown
dateCreated: 2023-02-27T12:33:35.792Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Building Multiplayer Games with TypeScript and WebSockets***English** document is available*](/en/Knowledge-base/TypeScript/building-multiplayer-games-with-typescript-and-websockets)
{.links-list}


# TypeScript와 WebSocket으로 멀티플레이어 게임 만들기

HTML5 표준 및 WebSocket 기술의 등장으로 멀티플레이어 게임 구축이 그 어느 때보다 쉬워졌습니다. 이 기사에서는 TypeScript와 WebSocket을 사용하여 간단한 멀티플레이어 게임을 만드는 방법을 살펴보겠습니다.

## 웹소켓이란?

WebSocket은 클라이언트와 서버 간의 양방향 통신을 가능하게 하는 프로토콜입니다. 전이중 통신이 가능하므로 데이터를 동시에 보내고 받을 수 있습니다.

WebSocket은 채팅 애플리케이션 및 온라인 게임과 같은 실시간 애플리케이션에 자주 사용됩니다. 또한 주식 거래와 같이 짧은 대기 시간이 필요한 애플리케이션에 매우 적합합니다.

## WebSocket 서버 설정

Node.js와 ws 라이브러리를 사용하여 WebSocket 서버를 설정합니다.

먼저 ws 라이브러리를 설치해야 합니다.

```
npm install ws
```

다음으로 server.ts라는 파일을 만들고 ws 라이브러리를 가져올 수 있습니다.

```typescript
import * as WebSocket from "ws";
```

그런 다음 WebSocket 서버를 만들고 포트 8080에서 수신 대기하도록 설정합니다.

```typescript
const wss = new WebSocket.Server({ port: 8080 });
```

이제 연결 이벤트에 대한 리스너를 추가할 수 있습니다. 이 이벤트는 클라이언트가 서버에 연결할 때 발생합니다.

```typescript
wss.on("connection", (ws: WebSocket) => {
  // ...
});
```

연결 리스너 내에서 메시지 이벤트에 대한 리스너를 추가할 수 있습니다. 이 이벤트는 클라이언트가 서버에 메시지를 보낼 때 발생합니다.

```typescript
wss.on("connection", (ws: WebSocket) => {
  ws.on("message", (message: string) => {
    // ...
  });
});
```

메시지 리스너 내에서 메시지를 처리하는 코드를 추가할 수 있습니다. 예를 들어 메시지를 콘솔에 출력할 수 있습니다.

```typescript
wss.on("connection", (ws: WebSocket) => {
  ws.on("message", (message: string) => {
    console.log(`Received message: ${message}`);
  });
});
```

마지막으로 닫기 이벤트에 대한 리스너를 추가할 수 있습니다. 이 이벤트는 클라이언트가 서버에서 연결을 끊을 때 발생합니다.

```typescript
wss.on("connection", (ws: WebSocket) => {
  ws.on("message", (message: string) => {
    console.log(`Received message: ${message}`);
  });

  ws.on("close", () => {
    // ...
  });
});
```

닫기 리스너 내에서 클라이언트가 사용한 모든 리소스를 정리하는 코드를 추가할 수 있습니다. 예를 들어 게임이나 채팅방에서 클라이언트를 제거할 수 있습니다.

```typescript
wss.on("connection", (ws: WebSocket) => {
  ws.on("message", (message: string) => {
    console.log(`Received message: ${message}`);
  });

  ws.on("close", () => {
    // remove client from game or chat room
  });
});
```

## WebSocket 클라이언트 생성

HTML5 WebSocket API를 사용하여 WebSocket 클라이언트를 생성합니다.

먼저 HTML 파일을 만들고 다음 스크립트를 포함해야 합니다.

```html
<script>
  const ws = new WebSocket("ws://localhost:8080");

  ws.onopen = () => {
    // ...
  };

  ws.onmessage = (event) => {
    // ...
  };

  ws.onclose = () => {
    // ...
  };
</script>
```

스크립트 내에서 WebSocket 인스턴스를 만들고 서버(ws://localhost:8080)에 연결합니다.

다음으로 open 이벤트에 대한 리스너를 추가할 수 있습니다. 이 이벤트는 연결이 설정되면 발생합니다.

```html
<script>
  const ws = new WebSocket("ws://localhost:8080");

  ws.onopen = () => {
    // ...
  };

  ws.onmessage = (event) => {
    // ...
  };

  ws.onclose = () => {
    // ...
  };
</script>
```

오픈 리스너 내에서 서버에 메시지를 보내는 코드를 추가할 수 있습니다.

```html
<script>
  const ws = new WebSocket("ws://localhost:8080");

  ws.onopen = () => {
    ws.send("Hello, world!");
  };

  ws.onmessage = (event) => {
    // ...
  };

  ws.onclose = () => {
    // ...
  };
</script>
```

다음으로 메시지 이벤트에 대한 리스너를 추가할 수 있습니다. 이 이벤트는 서버가 클라이언트에 메시지를 보낼 때 발생합니다.

```html
<script>
  const ws = new WebSocket("ws://localhost:8080");

  ws.onopen = () => {
    ws.send("Hello, world!");
  };

  ws.onmessage = (event) => {
    // ...
  };

  ws.onclose = () => {
    // ...
  };
</script>
```

메시지 리스너 내에서 메시지를 처리하는 코드를 추가할 수 있습니다. 예를 들어 메시지를 콘솔에 출력할 수 있습니다.

```html
<script>
  const ws = new WebSocket("ws://localhost:8080");

  ws.onopen = () => {
    ws.send("Hello, world!");
  };

  ws.onmessage = (event) => {
    console.log(`Received message: ${event.data}`);
  };

  ws.onclose = () => {
    // ...
  };
</script>
```

마지막으로 닫기 이벤트에 대한 리스너를 추가할 수 있습니다. 이 이벤트는 연결이 닫힐 때 발생합니다.

```html
<script>
  const ws = new WebSocket("ws://localhost:8080");

  ws.onopen = () => {
    ws.send("Hello, world!");
  };

  ws.onmessage = (event) => {
    console.log(`Received message: ${event.data}`);
  };

  ws.onclose = () => {
    // ...
  };
</script>
```

닫기 리스너 내에서 연결에 사용된 모든 리소스를 정리하는 코드를 추가할 수 있습니다. 예를 들어 게임이나 채팅방에서 클라이언트를 제거할 수 있습니다.

```html
<script>
  const ws = new WebSocket("ws://localhost:8080");

  ws.onopen = () => {
    ws.send("Hello, world!");
  };

  ws.onmessage = (event) => {
    console.log(`Received message: ${event.data}`);
  };

  ws.onclose = () => {
    // remove client from game or chat room
  };
</script>
```

## 간단한 멀티플레이어 게임 만들기

이제 WebSocket 서버와 클라이언트를 설정했으므로 이를 사용하여 간단한 멀티플레이어 게임을 만들 수 있습니다.

우리는 두 명의 플레이어가 번갈아 가며 X와 O를 3x3 그리드에 배치하는 게임을 만들 것입니다. 연속으로 3개의 X 또는 3개의 O를 배치하는 첫 번째 플레이어가 게임에서 승리합니다.

game.ts라는 파일을 만들고 Game 클래스를 정의하는 것으로 시작하겠습니다.

```typescript
class Game {
  // ...
}
```

Game 클래스 내에서 다음 속성을 정의합니다.

- 게임 보드를 나타내는 2D 배열
- 첫 번째 플레이어를 나타내는 player1 속성
- 두 번째 플레이어를 나타내는 player2 속성
- 차례가 된 플레이어를 나타내는 currentPlayer 속성

```typescript
class Game {
  board: string[][] = [
    ["", "", ""],
    ["", "", ""],
    ["", "", ""]
  ];

  player1: string;
  player2: string;
  currentPlayer: string;

  // ...
}
```

다음으로 Game 클래스의 생성자를 정의합니다. 생성자는 두 개의 플레이어 이름을 인수로 사용하고 player1, player2 및 currentPlayer 속성을 초기화합니다.

```typescript
class Game {
  board: string[][] = [
    ["", "", ""],
    ["", "", ""],
    ["", "", ""]
  ];

  player1: string;
  player2: string;
  currentPlayer: string;

  constructor(player1: string, player2: string) {
    this.player1 = player1;
    this.player2 = player2;
    this.currentPlayer = player1;
  }

  // ...
}
```

이제 placeMarker() 메서드를 정의하겠습니다. 이 메서드는 행과 열을 인수로 사용하고 현재 플레이어의 마커를 보드에 배치합니다.

```typescript
class Game {
  board: string[][] = [
    ["", "", ""],
    ["", "", ""],
    ["", "", ""]
  ];

  player1: string;
  player2: string;
  currentPlayer: string;

  constructor(player1: string, player2: string) {
    this.player1 = player1;
    this.player2 = player2;
    this.currentPlayer = player1;
  }

  placeMarker(row: number, col: number): void {
    this.board[row][col] = this.currentPlayer;
  }

  // ...
}
```

다음으로 checkWinner() 메서드를 정의합니다. 이 메서드는 현재 플레이어가 게임에서 이겼는지 확인합니다.

```typescript
class Game {
  board: string[][] = [
    ["", "", ""],
    ["", "", ""],
    ["", "", ""]
  ];

  player1: string;
  player2: string;
  currentPlayer: string;

  constructor(player1: string, player2: string) {
    this.player1 = player1;
    this.player2 = player2;
    this.currentPlayer = player1;
  }

  placeMarker(row: number, col: number): void {
    this.board[row][col] = this.currentPlayer;
  }

  checkWinner(): boolean {
    // check rows
    for (let row = 0; row < this.board.length; row++) {
      if (
        this.board[row][0] === this.currentPlayer &&
        this.board[row][1] === this.currentPlayer &&
        this.board[row][2] === this.currentPlayer
      ) {
        return true;
      }
    }

    // check columns
    for (let col = 0; col < this.board.length; col++) {
      if (
        this.board[0][col] === this.currentPlayer &&
        this.board[1][col] === this.currentPlayer &&
        this.board[2][col] === this.currentPlayer
      ) {
        return true;
      }
    }

    // check diagonals
    if (
      this.board[0][0] === this.currentPlayer &&
      this.board[1][1] === this.currentPlayer &&
      this.board[2][2] === this.currentPlayer
    ) {
      return true;
    }

    if (
      this.board[0][2] === this.currentPlayer &&
      this.board[1][1] === this.currentPlayer &&
      this.board[2][0] === this.currentPlayer
    ) {
      return true;
    }

    return false;
  }

  // ...
}
```

마지막으로 checkTie() 메서드를 정의합니다. 이 메서드는 게임이 동점인지 확인합니다.

```typescript
class Game {
  board: string[][] = [
    ["", "", ""],
    ["", "", ""],
    ["", "", ""]
  ];

  player1: string;
  player2: string;
  currentPlayer: string;

  constructor(player1: string, player2: string) {
    this.player1 = player1;
    this.player2 = player2;
    this.currentPlayer = player1;
  }

  placeMarker(row: number, col: number): void {
    this.board[row][col] = this.currentPlayer;
  }

  checkWinner(): boolean {
    // check rows
    for (let row = 0; row < this.board.length; row++) {
      if (
        this.board[row][0] === this.currentPlayer &&
        this.board[row][1] === this.currentPlayer &&
        this.board[row][2] === this.currentPlayer
      ) {
        return true;
      }
    }

    // check columns
    for (let col = 0; col < this.board.length; col++) {
      if (
        this.board[0][col] === this.currentPlayer &&
        this.board[1][col] === this.currentPlayer &&
        this.board[2][col] === this.currentPlayer
      ) {
        return true;
      }
    }

    // check diagonals
    if (
      this.board[0][0] === this.currentPlayer &&
      this.board[1][1] === this.currentPlayer &&
      this.board[2][2] === this.currentPlayer
    ) {
      return true;
    }

    if (
      this.board[0][2] === this.currentPlayer &&
      this.board[1][1] === this.currentPlayer &&
      this.board[2][0] === this.currentPlayer
    ) {
      return true;
    }

    return false;
  }

  checkTie(): boolean {
    for (let row = 0; row < this.board.length; row++) {
      for (let col = 0; col < this.board.length; col++) {
        if (this.board[row][col] === "") {
          return false;
        }
      }
    }

    return true;
  }
}
```

이제 Game 클래스를 정의했으므로 client.ts라는 파일을 만들고 가져올 수 있습니다.

```typescript
import { Game } from "./game";
```

다음으로 Game 인스턴스를 만들고 WebSocket 연결을 설정합니다.

```typescript
import { Game } from "./game";

const game = new Game("Player 1", "Player 2");

const ws = new WebSocket("ws://localhost:8080");

ws.onopen = () => {
  // ...
};

ws.onmessage = (event) => {
  // ...
};

ws.onclose = () => {
  // ...
};
```

오픈 리스너 내에서 플레이어 이름을 서버로 보내는 코드를 추가할 수 있습니다.

```타입스크립트
"./game"에서 { 게임 } 가져오기;

const game = new Game("플레이어 1", "플레이어 2");

const ws = new WebSocket("ws://localhost:8080");

ws.onopen = () => {
  ws.send(JSON.stringify({ type: "name", name: game.player1 }));
  승