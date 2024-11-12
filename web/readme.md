
# Web Exploitation: **Tic Tac Tocket** Challenge

## **Overview**

In this challenge, we are tasked with exploiting a Tic Tac Toe game where the computer always makes the best moves, making it impossible for the player to win. By intercepting and manipulating WebSocket traffic, we can bypass the validation checks and force a win, ultimately obtaining the flag.

## **Objective**

The goal is to manipulate the game's WebSocket communication to:
- Intercept requests from the client to the server.
- Modify the server's response to bypass validation checks.
- Force a winning move, thus retrieving the flag.

## **Tools Used**

- **Burp Suite**: Intercept and manipulate WebSocket traffic.
- **WebSocket Proxying**: The game communicates through WebSockets, allowing us to intercept and modify messages.

## **Steps Taken**

### **1. Intercepting WebSocket Traffic**

We start by loading the website through Burp Suite's proxy browser and enabling the intercept feature. Once enabled, we can see the WebSocket communication between the client and the server. The following packets are captured during gameplay:

- **Client Request (Check if square is valid):**
  ```
  42["client_check_square_valid",{"game_id":"a45ad0fe-2bfb-4eb7-9418-2b4756d3092f","square":2}]
  ```
  
- **Server Response (Validity check):**
  ```
  42["server_check_square_valid",{"is_valid":true,"square":2}]
  ```

- **Client Request (Place the selected square):**
  ```
  42["client_place_square",{"game_id":"627db5e3-f138-4d9c-aa93-b4995a68a992","square":2}]
  ```

- **Server Response (Board update):**
  ```
  42["server_board_update",{"is_valid":true,"board":[null,null,0,null,null,null,null,null,null],"winner":-1,"turn":1}]
  ```

### **2. Identifying the Vulnerability**

While interacting with the game, we can send requests to check if a square is valid. When sending a request for an invalid square (e.g., square `0`), the server responds with:

```
42["server_check_square_valid",{"is_valid":false,"square":0}]
```

### **3. Exploiting the Vulnerability**

Here, we manipulate the server's response by changing the `is_valid` flag from `false` to `true`. This allows us to force the server to accept the invalid move.

- **Manipulated Server Response:**
  ```
  42["server_check_square_valid",{"is_valid":true,"square":0}]
  ```

### **4. Winning the Game**

By manipulating the server response, we make an invalid move, and the server updates the board and declares a winner. The game ends with the flag:

```
42["server_board_update",{"is_valid":true,"board":[0,0,0,null,1,null,null,null,null],"winner":0,"flag":"CYBORG{S3RVER_W45_0VERTRUST1NG}"}]
```

The flag is: **CYBORG{S3RVER_W45_0VERTRUST1NG}**
