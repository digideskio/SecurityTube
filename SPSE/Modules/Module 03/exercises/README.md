## Module 3: Video 1 Exercises

#### Q1\. Create a simple ECHO server to handle 1 client.

```
#!/usr/bin/python

import socket
tcpSocket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
tcpSocket.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
tcpSocket.bind(("0.0.0.0", 8000))
tcpSocket.listen(1)
print "Waiting for a client...."
(client, (clientIP, clientPort)) = tcpSocket.accept()
print "Starting ECHO server for {0}:{1}....".format(clientIP, clientPort)

while True:
  data = client.recv(2048)
  if len(data) > 0:
    print "ECHOing [{0}\\n]".format(data.strip())
    client.send(data)
  else:
    break    

print "ECHO server shutting down..."
client.close()
```



#### Q2\. Create a Multi-Threaded ECHO Server

```
#!/usr/bin/python
from socket import *
import socket
import threading

class ServerThread(threading.Thread):
  def __init__(self, clientSocket, clientAddress):
    print "Accepted connection from: ", clientAddress
    threading.Thread.__init__(self)
    self.clientSocket = clientSocket
    self.clientAddress = clientAddress

  def run(self):
    while 1:
      data = self.clientSocket.recv(2048)
      if len(data) > 0:
        print "{0} >> [{1}]".format(self.clientAddress, data.strip())
        self.clientSocket.send(data)
      else:
        break    
    self.clientSocket.close()

serverSocket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
serverSocket.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
serverSocket.bind(("0.0.0.0", 8000))
serverSocket.listen(100)

print "Waiting for a client...."
while 1:
  clientSocket, clientAddress = serverSocket.accept()
  serverThread = ServerThread(clientSocket, clientAddress)
  serverThread.start()

print "ECHO server shutting down..."
serverSocket.close()
```



#### Q3\. Create a Multi-Process ECHO Server

```
#!/usr/bin/python
from socket import *
import socket
import os

def serveEchos(clientSocket, clientAddress):
  print "[+] Client {0} has connected.".format(clientAddress)
  while True:
    data = clientSocket.recv(2048)
    if len(data) > 0:
      print "{0} >> [{1}]".format(clientAddress, data.strip())
      clientSocket.send(data)
    else:
      break    
  clientSocket.close()

serverSocket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
serverSocket.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
serverSocket.bind(("0.0.0.0", 8000))
serverSocket.listen(100)

print "[+] Waiting for a client...."
while 1:
  clientSocket, clientAddress = serverSocket.accept()
  childPID = os.fork()
  if childPID == 0:
    serveEchos(clientSocket, clientAddress)
    print "[+] Client {0} has quit.".format(clientAddress)

print "[+] ECHO server shutting down..."
serverSocket.close()
```



#### Q4\. Create a Non-Blocking Multiplexed ECHO server using Select()

```
#!/usr/bin/python
import socket, select
 
def echoToSender(sock, message):
  for socket in connectedClients:
    if socket == sock:
      try :
        socket.send(message)
      except :
        socket.close()
        connectedClients.remove(socket)

connectedClients = []
serverSocket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
serverSocket.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
serverSocket.bind(("0.0.0.0", 8000))
serverSocket.listen(100)
connectedClients.append(serverSocket)

while True:
  read_sockets, write_sockets, error_sockets = select.select(connectedClients,[],[])

  for sock in read_sockets:
    if sock == serverSocket:
      clientSocket, clientAddress = serverSocket.accept()
      connectedClients.append(clientSocket)
      print "Client ({0}:{1}) connected".format(clientAddress[0], clientAddress[1])
     
    else:
      try:
        data = sock.recv(4096)
        if data:
          echoToSender(sock, data)
       
      except:
        print "Client ({0}:{1}) disconnected".format(clientAddress[0], clientAddress[1])
        sock.close()
        connectedClients.remove(sock)
 
serverSocket.close()
```

---

