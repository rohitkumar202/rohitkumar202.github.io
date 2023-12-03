# Threading

## Intro 
threads are python objects threading.Thread() class.

`current_thread()` retuns the current thread

```py
import threading
print(threading.current_thread())


output - <_MainThread(MainThread, started 139691228549120)>
```
threading id will differ on each execution

`is_alive()` - can be used to check if thread is started.

```py
import threading
print(threading.current_thread().is_alive())


output - True
```

## How to create threads

**Two ways of creating theads**
1. Using Thread class present in threading module
1. By extending Thread class

## Creating thread Using Thread Class

```py
from threading import Thread

def display(n, message):
    for i in range(n):
        print(message)

t1 = Thread(target=display, args=(4, "Hello World"))
t1.start()

output -

Hello World
Hello World
Hello World
Hello World
```

we can also use *kwargs* instead of *args*

```py
from threading import Thread

def display(n, message):
    for i in range(n):
        print(message)


t1 = Thread(target=display, kwargs={"n":4, "message":"Hello World"})
t1.start()
```

if we have some code after the main code, then both will execute parallely

```py
from threading import Thread

def display(n, message):
    for i in range(n):
        print(message)


t1 = Thread(target=display, kwargs={"n":14, "message":"Hello World"})
t1.start()

for i in range(10):
    print('Main thread code')

output - 
Hello World
Main thread code
Hello World
Hello World
Hello World
Main thread code
Main thread code
Main thread code
Main thread code
Main thread code
Main thread code
Main thread code
Main thread code
Main thread code
Hello World
Hello World
Hello World
Hello World
Hello World
Hello World
Hello World
Hello World
Hello World
Hello World
```

## Creating thread by extending Thread Class

```py
from threading import Thread

class MyThread(Thread):
    def run(self):
        for i in range(4):
            print("Hello world 2")

t1 = MyThread()
t1.start()        

output - 

Hello world 2
Hello world 2
Hello world 2
Hello world 2
```

using `__init__()` in `Thread()` Class
```py
from threading import Thread

class MyThread(Thread):
    def __init__(self):
        Thread.__init__(self)

    def run(self):
        for i in range(4):
            print("Hello world 2")

t1 = MyThread()
t1.start()        
```

pasing args to Class Constructor

```py
from threading import Thread

class MyThread(Thread):
    def __init__(self, n):
        self.n = n
        Thread.__init__(self)

    def run(self):
        for i in range(self.n):
            print("Hello world 2")

t1 = MyThread(5)
t1.start()        
```

Let's analyze the code below, there is no way for returng the result from the function

```py

from threading import Thread

def addition(a=5, b=7):
    print('the sum is ', a + b)
    return a + b

t1 = Thread(target=addition)
t1.start()        
```

## Displaying thread details

```py
from threading import Thread, main_thread, current_thread, active_count

def display():
    print('main thread details : ', main_thread())
    print('current thread details : ', current_thread())

    for i in range(5):
        print('thread running')

t1 = Thread(target=display)
t1.start()
print('active count : ', active_count())

output - 

main thread details :  <_MainThread(MainThread, started 139882820055040)>
active count :  2
current thread details :  <Thread(Thread-1 (display), started 139882807686720)>
thread running
thread running
thread running
thread running
thread running
```

using `enumerate()` to get list of running thread with details

```py
def display():
    print('main thread details : ', main_thread())
    print('current thread details : ', current_thread())

    for i in range(5):
        print('thread running')

t1 = Thread(target=display)
t1.start()
print('enumerate : ', enumerate())

output -

main thread details :  <_MainThread(MainThread, started 139682482536448)>
enumerate :  [<_MainThread(MainThread, started 139682482536448)>, <Thread(Thread-1 (display), started 139682469901888)>]
current thread details :  <Thread(Thread-1 (display), started 139682469901888)>
thread running
thread running
thread running
thread running
thread running
```

## Join() method

if thread wants to wait for some other thread, then we can use join() method



# Resources

- https://www.youtube.com/watch?v=vYKwSeXXzRw&list=PLI4OVrCFuY57b_16D8xs7-hmABHncVD_w&index=9
 
