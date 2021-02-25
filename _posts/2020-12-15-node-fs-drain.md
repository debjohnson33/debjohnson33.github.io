---
layout: post
title:      "Using Drain with the Node File System While Using a Write Stream"
date:       2020-12-15 09:50:48 +0000
---

The Node file system has an event called a ‘drain’ that is used to control a write stream for writing a large file. According to the documentation, ‘If a call to stream.write(chunk) returns false, the ‘drain’ event will be emitted when it is appropriate to resume writing data to the stream.’ This means that it only triggers when the write isn’t working and it has allowed for an appropriate amount of time so that you don’t end up with a ‘heap out of memory error’ and have to start the script again.

To use the drain, you put it within a loop. The examples show a do while loop.

This is after the write stream has been started:

```
const writeUsers = fs.createWriteStream(‘users.csv’);    // start the stream
writeUsers.write(‘id, username\n’, ‘utf8’);                       // write the headers

const writeTenMillionRecords(writer, encoding, callback) {
  let i = 10000000;
  let id = 0;
  function write() {
    let ok = true;
    do {
      i -= 1;  // incrementers
      id += 1;
      const username = faker.internet.userName();
      if (i === 0) {
        writer.write(data, encoding, callback);             // only call with the callback if i has reached 0
      } else {
        ok = writer.write(data, encoding);        // otherwise keep writing
      }
    } while (i < 0 && ok);     // if ok is false, the writing will pause until the ‘drain’ event is triggered
    if (i > 0) {
      writer.once(‘drain’, write);
    }
  }
write(); // call inner function
}
```

Invoke the function with a callback that has the ‘end’ method called on the write stream:

```
writeTenMillionRecords(writeUsers, ‘utf-8’ , () => {
  writeUsers.end();   // call end method on the write stream inside the callback function
});
```
