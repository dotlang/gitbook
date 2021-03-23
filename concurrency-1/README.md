# Concurrency



1. Using `result := expression` notation will initiate a new parallel task \(green thread\) as a child of the current task. Any access to the result `result` will block current process until the child is finished.
2. You can call core function to create a channel. Channels can be used for communication and synchronization across tasks.
3. A channel is represented via a generic struct with functions to read/write data \(Example A\).
4. Other operations like `select` are implemented as functions in std.

**Examples**

```perl
_ := process(10, 20)

channel = createChannel(int, 10)

#pass channel to a task
int_result := process(10, channel)

#write data into the channel (blocks if channel is full)
channel.write(100)

#read data from channel (blocks if there is nothing to read)
data = channel.read()
```

