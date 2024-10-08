# Backpressuring in Streams

The following is taken from this [link](https://nodejs.org/en/learn/modules/backpressuring-in-streams#backpressuring-in-streams) from the NodeJS documentation.

There is a general problem that occurs during data handling called backpressure and describes a buildup of data behind a buffer during data transfer. When the receiving end of the transfer has complex operations, or is slower for whatever reason, there is a tendency for data from the incoming source to accumulate, like a clog.

To solve this problem, there must be a delegation system in place to ensure a smooth flow of data from one source to another. Different communities have resolved this issue uniquely to their programs, `Unix pipes and TCP sockets are good examples of this`, and are often referred to as flow control. `In Node.js, streams have been the adopted solution`.

In a computer system, data is transferred from one process to another through pipes, sockets, and signals. In Node.js, we find a similar mechanism called Stream. Streams are great! `They do so much for Node.js and almost every part of the internal codebase utilizes that module`.

Usually NodeJS handles this for us under the hood. Keep the following in mind when you create custom streams. This is taken from this [link](https://nodejs.org/en/learn/modules/backpressuring-in-streams#rules-to-abide-by-when-implementing-custom-streams) from the documentation.

1. Never .push() if you are not asked.
2. Never call .write() after it returns false but wait for 'drain' instead.
3. Streams changes between different Node.js versions, and the library you use. Be careful and test things.

I found the 3rd point every where I read about high water mark and backpressure
