# Module 02 Notes

## System Programming

#### File I/O

- Opening a file
  - ```fd = open("filename.txt", "r")``` opens filename.txt for reading.
  - ```fd = open("filename.txt", "w")``` creates or overwrites filename.txt
  - ```fd = open("filename.txt", "a")``` opens existing filename.txt for writing to.
  - ```fd = open("filename.txt", "rw")``` creates a new filename.txt for reading and writing. 
- Writing to a file
  - ```fd.write("Write Test!")``` writes a test message to the file.
- Reading from a file
  - ```fileLines = fd.readLines()``` reads all lines from the file.
  - ```fileContents = fd.read(1024)``` reads up to 1024 bytes from the file.
- Closing a file descriptor
  - ```fd.close()``` closes the file to free up resources.
- Renaming from a file
  - ```os.rename("original-filename.txt", "new-filename.txt")```
- Deleting from a file
  - ```os.delete("filename.txt")```

#### Directory Navigation

- Get current working directory
  - ```os.getcwd()```
- Create new directory
  - ```os.mkdir("New-Directory")```
- View contents of directory
  - ```os.listdir("/home/root")```
- Check if file or directory:
  - ```os.path.isfile("/etc/hosts")``` returns True
  - ```os.path.isfile("/etc")``` returns True
  - ```os.path.isdir("/etc")``` returns True
  - ```os.path.isdir("/etc")``` returns False

#### Using glob to filter for specific files.

```
import os, glob

# Get all .py files in the etc directory
for item in glob.glob(os.path.join("/etc", "*.py")):
  print item
```

#### Forking

- Clones a process, creating identical process as the parent.
- ```fork()``` returns pid of child in the parent.
- ```fork()``` returns 0 in the child.
- Useful for providing tasks to child unrelated to parent process.
- Parent and child can communicate using IPC


#### Fork Demo

```
#!/usr/bin/python

import os

def forkDemo():
  childPID = os.fork()
  if childPID == 0:
    print "I am the child process! fork() returned pid {0}".format(childPID)
  else:
    print "I am the parent process! fork() returned pid {0}".format(childPID)

forkDemo()
```

#### Spawning new processes

- os.exec* family of functions
- Example: ```os.execvp("ping", ["ping", "127.0.0.1"])```
- Takes over process and will not return.


#### Threads

- Python is limited to one thread due to the "Global Interpreter Lock"
- If you are determined to use threads, look into the multiprocessing library.
- Simple threads use 'thread' module
- Advanced threading uses 'threading' module


#### Threading module example

```
#!/usr/bin/python
import threading
import Queue
import time

class WorkerThread(threading.Thread):
  def __init__(self, queue):
    threading.Thread.__init__(self)
    self.queue = queue

  def run(self):
    print "Starting WorkerThread"
    while True:
      counter = self.queue.get()
      print "Ordered to sleep for {0} seconds".format(counter)
      time.sleep(counter)
      print "Finished sleeping for {0} seconds".format(counter)
      self.queue.task_done()


queue = Queue.Queue()
for i in range(10):
  print "Creating WorkerThread {0}".format(i)
  worker = WorkerThread(queue)
  worker.setDaemon(True)
  worker.start()
  print "Created WorkerThread {0}".format(i)

for j in range(10):
  queue.put(j)

queue.join()
print "All Tasks Complete!"  
```


#### Signals and IPC

- Allows handling of asynchronous events


#### Signal module example

```
#!/usr/bin/python
import signal

def signalHandler(signalNumber, stackFrame):
  print "Caught ctrl+c signal. Ignoring."
  
signal.signal(signal.SIGINT, signalHandler)
while True:
  pass
```


#### Subprocess

- Ability to run program and use the output in your program.
- ```subprocess.call(['ps', 'aux'])```
- ```subprocess.check_output(['ls','-al'])```


#### Subprocess Module Example 1: Reading from a process' stdin using check_output

```
#!/usr/bin/python
import subprocess

lines = subprocess.check_output(['ls', '-al'])
lines = lines.split('\n')

```

#### Subprocess Module Example 1: Reading from a process' stdin using Popen

```
#!/usr/bin/python
import subprocess

handle = subprocess.Popen("ls", stdin=subprocess.PIPE, stdout=subprocess.PIPE, stderr=subprocess.PIPE, close_fds=True)
handle.stdout.read()
```

