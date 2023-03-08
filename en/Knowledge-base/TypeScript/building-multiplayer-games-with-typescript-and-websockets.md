---
title: Building Multiplayer Games with TypeScript and WebSockets
description: 
published: true
date: 2023-02-27T12:33:37.231Z
tags: 
editor: markdown
dateCreated: 2023-02-27T12:33:35.794Z
---

- [TypeScript 및 WebSocket으로 멀티플레이어 게임 구축***Korean** document is available*](/ko/Knowledge-base/TypeScript/building-multiplayer-games-with-typescript-and-websockets)
{.links-list}


# Building Multiplayer Games with TypeScript and WebSockets

With the rise of the HTML5 standard and WebSocket technology, building multiplayer games has never been easier. In this article, we'll explore how to use TypeScript and WebSockets to create a simple multiplayer game.

## What is WebSocket?

WebSocket is a protocol that enables two-way communication between a client and a server. It allows for full-duplex communication, meaning that data can be sent and received simultaneously.

WebSockets are often used for real-time applications, such as chat applications and online games. They are also well-suited for applications that require low latency, such as stock trading.

## Setting up a WebSocket Server

We'll use Node.js and the ws library to set up a WebSocket server.

First, we need to install the ws library:

```
npm install ws
```

Next, we can create a file called server.ts and import the ws library:

```typescript
import * as WebSocket from "ws";
```

Then, we'll create a WebSocket server and set it to listen on port 8080:

```typescript
const wss = new WebSocket.Server({ port: 8080 });
```

Now, we can add a listener for the connection event. This event is emitted when a client connects to the server:

```typescript
wss.on("connection", (ws: WebSocket) => {
  // ...
});
```

Within the connection listener, we can add a listener for the message event. This event is emitted when a client sends a message to the server:

```typescript
wss.on("connection", (ws: WebSocket) => {
  ws.on("message", (message: string) => {
    // ...
  });
});
```

Within the message listener, we can add code to handle the message. For example, we can print the message to the console:

```typescript
wss.on("connection", (ws: WebSocket) => {
  ws.on("message", (message: string) => {
    console.log(`Received message: ${message}`);
  });
});
```

Finally, we can add a listener for the close event. This event is emitted when a client disconnects from the server:

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

Within the close listener, we can add code to clean up any resources that were used by the client. For example, we can remove the client from a game or chat room:

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

## Creating a WebSocket Client

We'll use the HTML5 WebSocket API to create a WebSocket client.

First, we need to create an HTML file and include the following script:

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

Within the script, we create a WebSocket instance and connect it to our server (ws://localhost:8080).

Next, we can add a listener for the open event. This event is emitted when the connection is established:

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

Within the open listener, we can add code to send a message to the server:

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

Next, we can add a listener for the message event. This event is emitted when the server sends a message to the client:

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

Within the message listener, we can add code to handle the message. For example, we can print the message to the console:

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

Finally, we can add a listener for the close event. This event is emitted when the connection is closed:

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

Within the close listener, we can add code to clean up any resources that were used by the connection. For example, we can remove the client from a game or chat room:

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

## Creating a Simple Multiplayer Game

Now that we've set up a WebSocket server and client, we can use them to create a simple multiplayer game.

We'll create a game where two players take turns placing X's and O's on a 3x3 grid. The first player to place three X's or three O's in a row wins the game.

We'll start by creating a file called game.ts and defining a Game class:

```typescript
class Game {
  // ...
}
```

Within the Game class, we'll define the following properties:

- A 2D array to represent the game board
- A player1 property to represent the first player
- A player2 property to represent the second player
- A currentPlayer property to represent the player who's turn it is

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

Next, we'll define a constructor for the Game class. The constructor will take two player names as arguments and initialize the player1, player2, and currentPlayer properties:

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

Now, we'll define a placeMarker() method. This method will take a row and column as arguments and place the current player's marker on the board:

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

Next, we'll define a checkWinner() method. This method will check if the current player has won the game:

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

Finally, we'll define a checkTie() method. This method will check if the game is a tie:

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

Now that we've defined the Game class, we can create a file called client.ts and import it:

```typescript
import { Game } from "./game";
```

Next, we'll create a Game instance and set up a WebSocket connection:

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

Within the open listener, we can add code to send the player names to the server:

```typescript
import { Game } from "./game";

const game = new Game("Player 1", "Player 2");

const ws = new WebSocket("ws://localhost:8080");

ws.onopen = () => {
  ws.send(JSON.stringify({ type: "name", name: game.player1 }));
  w