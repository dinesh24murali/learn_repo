# Buffers and streams in Node.js

This is a copy of a good article from [medium](https://medium.com/@diego.coder/buffers-and-streams-in-node-js-8cf094621dd9).

Basic article on managing Buffers and Streams in Nodejs. Concepts and implementations.

## Introduction

The concept of Buffers and Streams in the world of computing and communications is not something new. Many times we have heard the word Streaming when, for example, a famous video game player invites you to follow a live broadcast, or when a person transmits a live broadcast via Instagram or Facebook. Streaming videos or others follow the same principles that we will check below.

## Buffer concept

A buffer is a space in memory (usually RAM) that temporarily stores binary data. The purpose of this space is to help any running entity not lose data during a transfer using a FIFO system.

## Buffer in Nodejs

In Nodejs we can manipulate these memory spaces with the module called Buffer built into its core. Buffers are widely used when working with binary data at the network level. `Let us remember that many of the Nodejs modules and functionalities work implicitly based on events and manipulation of Buffer / Streams, such as the core File System or HTTP modules that store the temporary data flow in a Buffer`.

Here are some important features of Buffers:

- Buffers are stored in a sequence of integers.
- Once created they cannot be resized.

Here is an example of creating a Buffer in Nodejs using the Buffer class:

```js
const { Buffer } = require("buffer");
const buf6 = Buffer.from("hello");

console.log(buf6);
```

The code snippet above creates a Buffer containing the UTF-8 encoded bytes for the string “hello”, this prints the following output to the console:

```bash
<Buffer 68 65 6c 6c 6f>
hello
// [0x68, 0x65, 0x6c, 0x6c, 0x6f] (hexadecimal notation)
```

Once the information is saved, we can perfectly read the stored content, here is an example:

```js
const text = buf6.toString();
console.log(text); // hello
```

`Most of the programming languages have incorporated in their core a set of functionalities and classes that allow you to work with Buffers and Streams in a simple way`.

## Stream concept

They are information flows that are used in the transmission of binary data. They are also a way to handle network communications or any kind of back-and-forth data exchange efficiently, by breaking information down into smaller pieces.

Here are some important features of Streams:

- Streams work sequentially.
- The information is transmitted through “chunks” (pieces).
- Streams rely on buffers to manage content.

Let us emphasize that Streams are one of the most effective strategies for processing large amounts of information. For example, when the size of a file is larger than the free space in memory, the use of smaller pieces makes it possible to read it.

Streaming services like Netflix or others do not force you to download the video in one go, as it would be a very expensive process for the device. Instead, these services send the information to you in a continuous stream of chunks, allowing you to play the content immediately.

## Stream in Nodejs

Nodejs has a module called stream that helps us with the manipulation of these flows, but depending on the case we will use some type of stream.

In general, there are 4 types of Streams in Nodejs:

- `Writable`: Streams in which we can write data.
- `Readable`: Streams receiving input data.
- `Duplex`: Streams that are both read and written.
- `Transform`: Streams that can modify or transform data as it is written and read.

If we have already worked with Nodejs before, surely we have noticed that, for example, any HTTP server based on Nodejs, works with reading Streams in the request to the server (Readable) and the response to the client works with writing Streams (Writable). This and other core modules work in the same way.

Here is an example of creating a stream in Nodejs of type readable and sending data:

```js
const Stream = require("stream");
const readableStream = new Stream.Readable();

readableStream.push("Hello");
readableStream.push(" ");
readableStream.push("World");
readableStream.push(null);

async function getContentReadStream(readable) {
  for await (const chunk of readable) {
    console.log(chunk);
    console.log(chunk.toString());
  }
}

getContentReadStream(readableStream);
```

This prints the following output to the console:

```
<Buffer 48 65 6c 6c 6f 20 57 6f 72 6c 64>
Hello World
```

Emphasizing that when creating an object of type stream, a support buffer for manipulation is automatically created. The size of the chunk or buffer can be previously configured.

Here is a complementary image of the Buffers and Streams relationship:
![Kibana](./buffer.webp "Kibana1")
Resources Nodejs Buffers and Streams

[Buffer API](https://nodejs.org/api/buffer.html): Documentation and characteristics of the Buffers.
[Stream API](https://nodejs.org/api/stream.html): Documentation and characteristics of the Streams.
## Ending
Buffer and Stream handling are the most powerful core features of Nodejs. Input and output operations are optimized under easy-to-process pipelined sequences, helping the system consume large amounts of information without risking processing.

## Piping Streams

Piping allows you to connect multiple streams together. For instance, you can read data from one stream and write it directly to another.

```js
const fs = require('fs');

// Create a readable stream
const readableStream = fs.createReadStream('source.txt');

// Create a writable stream
const writableStream = fs.createWriteStream('destination.txt');

// Pipe the readable stream into the writable stream
readableStream.pipe(writableStream);

// Handle the 'finish' event to know when piping is complete
writableStream.on('finish', () => {
  console.log('Piping finished.');
});
```
