---
layout: post
title:      "jQuery Ajax and Node Server"
date:       2020-10-27 09:50:48 +0000
---

One of the challenges I had recently was how to apply my understanding of the straight Node implementation of a server (versus using Express) and the use of the jQuery ajax to make requests to the server. I knew that the ‘endpoint’ of both of them had to match up with each other, but in working with my pair, we had a hard time figuring out how to do it. After a lot of review of various resources on these two subjects, we were able to apply what was needed to get a client and server ‘talking’ to each other. On the client side, a jQuery ajax request looks something like this:

```
$.ajax({
      type: ‘GET’
      url: serverUrl, <-----This would be the http://127.0.0.1:3000 or whatever port the server is on
      success: (direction) => {
        SwimTeam.move(direction);
      },
      complete: () => {
        setTimeout(fetchCommand, 50);
      }
});
```

In order to respond with the correct information, the url for each should match. If it's the main page, then it corresponds to the ‘/’.

```
if (req.method === 'GET') {
    if (req.url === '/') {
      res.writeHead(200, headers);
      var command = messageQueue.dequeue();
      if (command) {
        console.log('Responding with:', command);
        res.end(command);
      } else {
        res.end();
      }
}
```

For other routes, the url property in the ajax would need to match. For example ‘/books’ would need to be the value of req.url and would be added as an additional check in the if statement.

```
if (req.method === ‘GET’ && ‘/books’)
```

Or

```
if (req.method === ‘GET’) {
  if (req.url === ‘/books’) {
   // respond with books
  }
}
```
