# Module 03 Notes

##Network Programming

####Sockets

- TCP and UDP Sockets used for regular servers and clients.
- Raw Sockets used for sniffing and injection
- We use python's ```socket``` module


####Sample ECHO Server

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


##Sample ECHO Server Explained

####```socket.socket(socket.AF_INET, socket.SOCK_STREAM)```
- ```socket.socket()``` - Creates the socket we will communicate over.
- ```socket.AF_INET``` - Address family.
- ```socket.SOCK_STREAM``` - TCP socket.


####```tcpSocket.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)```
- ```tcpSocket.setsockopt()``` - manipulate options for the socket
- ```socket.SOL_SOCKET``` - Specify that we are configuring a socket.
- ```socket.SO_REUSEADDR``` - Allows other sockets to bind() to this port if there is no active socket already.
- ```1``` - The value we want to set the option to. In this case, enable.


####```tcpSocket.bind(("0.0.0.0", 8000))```
- ```tcpSocket.bind()``` - Ties the socket to an interface and port
- ```"0.0.0.0"``` - The IP address of the interface we want to listen on
- ```8080``` - The port to listen on


####```tcpSocket.listen(2)```
- ```tcpSocket.listen()``` - Prepare to start listening for incoming connections.
- ```2``` - The number of concurrent connections we can handle.


####```(client, (ip, port)) = tcpSocket.accept()```
- ```tcpSocket.accept()``` - 
- ```client``` - Socket we can use to talk to the client.
- ```ip``` - IP Address of the client
- ```port``` - Port the client connected from.


####```data = client.recv(2048)```
- ```data = client.recv()``` - Receives data from the client. 
- ```data``` - The data received by the server from the client.
- ```2048``` - Size of the buffer to receive.


####```client.send(data)```
- ```client.send()``` - Sends data to the client. Returns num bytes sent.
- ```data``` - The data to send to the client from the server.


####```client.close()```
- ```client.close()``` - Close the connection between the client and server.



##Handling Client Connections

####Options for processing clients
- One at a time
- Multi-Threaded Server
- Multi-Process Server
- Non-Blocking Sockets with Select (Multiplexing)


####Sample Client Program

```
import socket
import sys

tcpSocket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
tcpSocket.connect((sys.argv[1], sys.argv[2]))

while 1:
  userInput = raw_input("out> ")
  tcpSocket.send(userInput)
  print "in> {0}".format(tcpSocket.recv(2048))

tcpSocket.close()
```



##SocketServer Framework

####About SocketServer Framework
- Creates TCP and UDP servers
- Does all the basic steps for you in the background

####SocketServer Usage
- Has to be a subclass of ```BaseRequestHandler```
- Override ```handle()``` to process request
- Can ```handle_request``` or ```serve_forever```
- ```self.request``` is the client socket we can send/receive to and from
- ```self.client_address``` is the client details

####SocketServer Sample Program

```
import SocketServer

class EchoHandler(SocketServer.BaseRequestHandler):
  def handle(self):
    print "Client connected: {0}".format(self.client_address)
    data = "dummy"
    while len(data):
      data = self.request.recv(1024)
      self.request.send(data)
    print "Client disconnected: {0}".format(self.client_address)

serverAddress = ("0.0.0.0", 9000)
server = SocketServer.TCPServer(serverAddress, EchoHandler)
server.serve_forever()
```



##SocketServer Sample Program Explained

####```serverAddress = ("0.0.0.0", 9000)```
- Server will listen on all address at port 9000

####```server = SocketServer.TCPServer(serverAddress, EchoHandler)```
- ```SocketServer.TCPServer()``` - Start a TCP Server
- ```serverAddress``` - A tuple containing server address and port
- ```EchoHandler``` - The class which will handle the requests.

####```server.serve_forever()```
- ```server.serve_forever()``` - Serves clients forever
- ```server.handle_request()``` - Serves a single request


