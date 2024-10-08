---
title: >-
  Using Python 2 create TCP sockets
date: 2024-10-07 21:59:18
tags:
---

1. Import Necessary Modules:
Python

import socket

Use code with caution.

2. Create a Socket Object:
Python

sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

Use code with caution.

    socket.AF_INET: Specifies the Internet Protocol (IP) family for network communication.
    socket.SOCK_STREAM: Indicates that you're using a TCP socket for reliable, connection-oriented communication.

3. Bind the Socket to an Address and Port:
Python

server_address = ('localhost', 12345)
sock.bind(server_address)

Use code with caution.

    server_address: A tuple containing the IP address (or hostname) and port number where the server will listen for connections.
    sock.bind(): Associates the socket with the specified address and port.

4. Listen for Incoming Connections:
Python

sock.listen(1)

Use code with caution.

    sock.listen(): Sets the maximum number of connections that can be pending at once. In this case, it's set to 1.

5. Accept Incoming Connections:
Python

while True:
    connection, client_address = sock.accept()
    print(f"Connection from {client_address}")

    # Process data from the client
    data = connection.recv(1024)
    if not data:
        break
    print(f"Received: {data}")

    # Send a response back to the client
    message = b"Hello, world!"
    connection.sendall(message)

    connection.close()
