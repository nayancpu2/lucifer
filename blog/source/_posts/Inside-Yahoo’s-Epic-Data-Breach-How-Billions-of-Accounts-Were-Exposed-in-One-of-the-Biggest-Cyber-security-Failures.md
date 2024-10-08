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
