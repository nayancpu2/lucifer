---
title: >-
  Using Python 2 create TCP sockets
date: 2024-10-07 21:59:18
tags:
---

To create a TCP connection using Python, you can use the built-in socket library. Here’s a simple example that demonstrates how to create both a TCP client and server. 

[TCP Server]


```
import socket

def tcp_server(host='127.0.0.1', port=65432):
    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as server_socket:
        server_socket.bind((host, port))
        server_socket.listen()
        print(f'Server listening on {host}:{port}')

        conn, addr = server_socket.accept()
        with conn:
            print(f'Connected by {addr}')
            while True:
                data = conn.recv(1024)
                if not data:
                    break
                print(f'Received: {data.decode()}')
                conn.sendall(data)  # Echo back the received data

if __name__ == '__main__':
    tcp_server()
```
TCP Client

```
import socket

def tcp_client(host='127.0.0.1', port=65432):
    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as client_socket:
        client_socket.connect((host, port))
        message = 'Hello, Server!'
        client_socket.sendall(message.encode())
        data = client_socket.recv(1024)
        print(f'Received from server: {data.decode()}')

if __name__ == '__main__':
    tcp_client()
```

How to Run

  Start the Server:
        Save the server code in a file named tcp_server.py.
        Run it in your terminal: 

```
        python tcp_server.py
```

Start the Client:

  Save the client code in a file named tcp_client.py.
    In a new terminal, run:
```
python tcp_client.py

```
