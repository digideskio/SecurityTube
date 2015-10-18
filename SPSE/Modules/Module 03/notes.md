# Module 03 Notes

## Network Programming

#### Sockets

- TCP and UDP Sockets used for regular servers and clients.
- Raw Sockets used for sniffing and injection
- We use python's ```socket``` module


#### Sample ECHO Server

```
#!/usr/bin/python

import socket

tcpSocket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
tcpSocket.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
tcpSocket.bind(("0.0.0.0", 8000))
tcpSocket.listen(2)

print "Waiting for a client...."

clientConnection = tcpSocket.accept()
(client, (ip, port)) = clientConnection

print "Received connection from: {0}".format(ip)
print "Starting ECHO output...."

data = "dummy"
while len(data):
  data = client.recv(2048)
  print "Client sent: {0}".format(data)
  client.send(data)


print "Closing connection...."
client.close()
```


## Sample ECHO Server Explained

#### ```socket.socket(socket.AF_INET, socket.SOCK_STREAM)```
- ```socket.socket()``` - Creates the socket we will communicate over.
- ```socket.AF_INET``` - Address family.
- ```socket.SOCK_STREAM``` - TCP socket.


#### ```tcpSocket.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)```
- ```tcpSocket.setsockopt()``` - manipulate options for the socket
- ```socket.SOL_SOCKET``` - Specify that we are configuring a socket.
- ```socket.SO_REUSEADDR``` - Allows other sockets to bind() to this port if there is no active socket already.
- ```1``` - The value we want to set the option to. In this case, enable.


#### ```tcpSocket.bind(("0.0.0.0", 8000))```
- ```tcpSocket.bind()``` - Ties the socket to an interface and port
- ```"0.0.0.0"``` - The IP address of the interface we want to listen on
- ```8080``` - The port to listen on


#### ```tcpSocket.listen(2)```
- ```tcpSocket.listen()``` - Prepare to start listening for incoming connections.
- ```2``` - The number of concurrent connections we can handle.


#### ```(client, (ip, port)) = tcpSocket.accept()```
- ```tcpSocket.accept()``` - 
- ```client``` - Socket we can use to talk to the client.
- ```ip``` - IP Address of the client
- ```port``` - Port the client connected from.


#### ```data = client.recv(2048)```
- ```data = client.recv()``` - Receives data from the client. 
- ```data``` - The data received by the server from the client.
- ```2048``` - Size of the buffer to receive.


#### ```client.send(data)```
- ```client.send()``` - Sends data to the client. Returns num bytes sent.
- ```data``` - The data to send to the client from the server.


#### ```client.close()```
- ```client.close()``` - Close the connection between the client and server.



## Handling Client Connections

#### Options for processing clients
- One at a time
- Multi-Threaded Server
- Multi-Process Server
- Non-Blocking Sockets with Select (Multiplexing)
