## Module 2: Video 1 Exercises

#### Q1\. Read /var/log/messages

```
#!/usr/bin/python

# On OS X, the /var/log/messages equivalent is /var/log/system.log
logFileDescriptor = open("/var/log/system.log", "r")
for line in logFileDescriptor.readlines():
  print line.strip()
logFileDescriptor.close()
```



#### Q2\. Find all the logs in it which pertain to USB and print them out selectively.

```
#!/usr/bin/python

# On OS X, the /var/log/messages equivalent is /var/log/system.log
logFileDescriptor = open("/var/log/system.log", "r")
for line in logFileDescriptor.readlines():
  if "USB" in line.upper():
    print line.strip()
logFileDescriptor.close()
```

---

## Module 2: Video 2 Exercises

#### Q1\. Create a program which can recursively traverse directories and print the file listing in a hierarchical way.

Example:

```
A
----a.txt
----b.txt
----B
--------c.out
```

Solution:

```
#!/usr/bin/python
###############################################################
# dir-walker by rot0xd                                        #
#-------------------------------------------------------------#
# Displays files under the provided directory in a tree       #
# structure for hierarchical viewing.                         #
#                                                             #
# Usage: ./dir-walk <directory>                               #
#                                                             #
# Note: Could have used os.walk() but wanted to limit myself  #
#       to functionality taught in the SPSE course.           #
###############################################################

import sys, os

def printDirectory(directoryName, depth=0):
  indentation = "-" * (2 * (depth + 1))

  # Verify existence of directory.
  if not os.access(directoryName, os.F_OK):
    print "{0}[!] Cannot find directory '{1}'".format(indentation, directoryName)
    return

  os.chdir(directoryName)
  directoryName = os.getcwd()
  indentation = "-" * (2 * (depth + 1))

  for entry in os.listdir(directoryName):
    absolutePath = "{0}/{1}".format(directoryName, entry)
    print "{0}{1}".format(indentation, entry)
    if os.path.isdir(absolutePath):
      printDirectory(absolutePath, depth=(depth+1))


if len(sys.argv) != 2:
  print "Usage: {0} <directory>".format(sys.argv[0])
else:
  printDirectory(sys.argv[1])
```

#### Q2\. For any given filename, list out all the stats related to the file such as size, creation time, path, etc.

```
#!/usr/bin/python
###############################################################
# file-info-viewer by rot0xd                                  #
#-------------------------------------------------------------#
# Displays all information about the file provided through    #
# python's os.path module.                                    #
#                                                             #
# Usage: ./file-info-viewer <filename>                        #
###############################################################

import sys, os

def printFileInfo(filename):
  # Verify existence of directory.
  if not os.access(filename, os.F_OK):
    print "[!] Cannot find file '{0}'".format(directoryName)
    return

  print "{0}".format(filename)
  print "------------------------------------------------------"
  print "abspath: {0}".format(os.path.abspath(filename))
  print "basename: {0}".format(os.path.basename(filename))
  print "commonprefix: {0}".format(os.path.commonprefix(filename))
  print "dirname: {0}".format(os.path.dirname(filename))
  print "exists: {0}".format(os.path.exists(filename))
  print "expanduser: {0}".format(os.path.expanduser(filename))
  print "expandvars: {0}".format(os.path.expandvars(filename))
  print "getatime: {0}".format(os.path.getatime(filename))
  print "getctime: {0}".format(os.path.getctime(filename))
  print "getmtime: {0}".format(os.path.getmtime(filename))
  print "getsize: {0}".format(os.path.getsize(filename))
  print "isabs: {0}".format(os.path.isabs(filename))
  print "isdir: {0}".format(os.path.isdir(filename))
  print "isfile: {0}".format(os.path.isfile(filename))
  print "islink: {0}".format(os.path.islink(filename))
  print "ismount: {0}".format(os.path.ismount(filename))
  print "join: {0}".format(os.path.join(filename))
  print "lexists: {0}".format(os.path.lexists(filename))
  print "normcase: {0}".format(os.path.normcase(filename))
  print "normpath: {0}".format(os.path.normpath(filename))
  print "realpath: {0}".format(os.path.realpath(filename))
  print "relpath: {0}".format(os.path.relpath(filename))
  print "split: {0}".format(os.path.split(filename))
  print "splitdrive: {0}".format(os.path.splitdrive(filename))
  print "splitext: {0}".format(os.path.splitext(filename))

if len(sys.argv) != 2:
  print "Usage: {0} <filename>".format(sys.argv[0])
else:
  printFileInfo(sys.argv[1])
```

---

## Module 2: Video 4 Exercises

#### Q1\. Based on the knowledge you have gained in the network programming module, create a multi-threaded port scanner in Python which uses SYN scanning.

```
TODO: Will return after completion of network security module
```

---

## Module 2: Video 5 Exercises

#### Q1\. Create a list of 10 FTP sites. Use WorkerThreads and a Queue which can login to these sites and list the root directory and then exit. Use 5 threads for this job.

```
TODO: Will return after completion of network security module
```

#### Q2\. There is a locking mechanism available in the Thread class which you can use to lock resources for dedicated use. Create a sample code to illustrate this concept.

```
#!/usr/bin/python

import threading
import thread
import time

class RespectfulWorkerThread(threading.Thread):
  def __init__(self, lock=None, wait=False):
    threading.Thread.__init__(self)
    self.lock = lock
    self.wait = wait

  def run(self):
    if self.wait:
      self.lock.acquire_lock()

    for i in range(1, 6):
      print i
      time.sleep(1)
  
    if self.wait:
      self.lock.release_lock()

#########################################################

print "Threads without locks:"
threads = []
for i in range(1,11):
  worker = RespectfulWorkerThread()
  worker.setDaemon(True)
  worker.start()
  threads.append(worker)

for currentThread in threads:
  currentThread.join()

#########################################################

print "Threads with locks:"
threads = []
threadLock = thread.allocate_lock()
for i in range(1,3):
  worker = RespectfulWorkerThread(threadLock, wait=True)
  worker.setDaemon(True)
  worker.start()
  threads.append(worker)

for thread in threads:
  thread.join()
```

#### Q3\. Explore the multiprocessing module in Python. How does it leverage multi-core setups? Program the TCP SYN scanner using multiprocessing.

```
TODO: Will return after completion of network security module
```

---

## Module 2: Video 6 Exercises

#### Q1\. Create a TCP server which listens to a port. Implement signals to ensure it automatically shuts down after a pre-configured duration which is given via command line. Example: "./tcp-server -s 100" shuts down after listening on the port for 100 seconds. Hint: Use SIGALARM

```
TODO: Will return after completion of network security module
```
