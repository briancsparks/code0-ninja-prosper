---
title: "Background"
date: 2020-09-06T18:48:21-07:00
weight: 10
draft: true
---

Like everyone else, I have spent a lot of time Googling and on [Stack Overflow](https://stackoverflow.com/questions/11828270/how-do-i-exit-the-vim-editor/11828573), [Geeks for Geeks](https://www.geeksforgeeks.org/),
and the like to find out how to do something specific in whatever language I was using at the time. It's
great that you can get a lot of your work done just by copying work someone else has done, and
they are happy that their work is being copied, so there's no guilt :).

And then I saw an [example](https://github.com/mscdex/ssh2 (npm install ssh2)) that inspired this site. It is from the `ssh2` Node.js package. On the repo's
main page are several examples of how to use the library. The special thing is that they are not just
little snippets, like you usually get on the Internet. They are whole programs, and they work without
any other effort to build the code around it.

They didn't work exactly for my needs, but it was a thousand times easier to delete the part(s) I
didn't need, than it would be to go back and begin another search for the missing parts.

So, that's what this site is: template **code** that has **zero** extra effort to use, so you can be a **ninja**.

I have copied 2 examples here so you can see what I mean. You don't need to know Javascript or
Node.js -- just look at the fact that the code is 'the whole thing,' and that you wouldn't need to
put work into filling the missing parts, you just delete what you don't need.

### From the ssh2 Github Repo

I highly encourage you to visit the [ssh2](https://github.com/mscdex/ssh2 (npm install ssh2)) site,
but here are a few eamples for you to enjoy.

Notice that it's all there. Error handling, closing connections. Function parameters are filled
in with something reasonable, so you can see an example of correct usage. When a file has to be
read, the template doesn't just tell you that you will have to read a file, it actually provides
the code to read the file.

#### Connection Hopping

```javascript
var Client = require('ssh2').Client;
 
var conn1 = new Client();
var conn2 = new Client();
 
// Checks uptime on 10.1.1.40 via 192.168.1.1
 
conn1.on('ready', function() {
  console.log('FIRST :: connection ready');
  // Alternatively, you could use netcat or socat with exec() instead of
  // forwardOut()
  conn1.forwardOut('127.0.0.1', 12345, '10.1.1.40', 22, function(err, stream) {
    if (err) {
      console.log('FIRST :: forwardOut error: ' + err);
      return conn1.end();
    }
    conn2.connect({
      sock: stream,
      username: 'user2',
      password: 'password2',
    });
  });
}).connect({
  host: '192.168.1.1',
  username: 'user1',
  password: 'password1',
});
 
conn2.on('ready', function() {
  console.log('SECOND :: connection ready');
  conn2.exec('uptime', function(err, stream) {
    if (err) {
      console.log('SECOND :: exec error: ' + err);
      return conn1.end();
    }
    stream.on('end', function() {
      conn1.end(); // close parent (and this) connection
    }).on('data', function(data) {
      console.log(data.toString());
    });
  });
});
```

#### Password and public key authentication and non-interactive (exec) command execution

```javascript
var fs = require('fs');
var crypto = require('crypto');
var inspect = require('util').inspect;

var ssh2 = require('ssh2');
var utils = ssh2.utils;

var allowedUser = Buffer.from('foo');
var allowedPassword = Buffer.from('bar');
var allowedPubKey = utils.parseKey(fs.readFileSync('foo.pub'));

new ssh2.Server({
  hostKeys: [fs.readFileSync('host.key')]
}, function(client) {
  console.log('Client connected!');

  client.on('authentication', function(ctx) {
    var user = Buffer.from(ctx.username);
    if (user.length !== allowedUser.length
        || !crypto.timingSafeEqual(user, allowedUser)) {
      return ctx.reject();
    }

    switch (ctx.method) {
      case 'password':
        var password = Buffer.from(ctx.password);
        if (password.length !== allowedPassword.length
            || !crypto.timingSafeEqual(password, allowedPassword)) {
          return ctx.reject();
        }
        break;
      case 'publickey':
        var allowedPubSSHKey = allowedPubKey.getPublicSSH();
        if (ctx.key.algo !== allowedPubKey.type
            || ctx.key.data.length !== allowedPubSSHKey.length
            || !crypto.timingSafeEqual(ctx.key.data, allowedPubSSHKey)
            || (ctx.signature && allowedPubKey.verify(ctx.blob, ctx.signature) !== true)) {
          return ctx.reject();
        }
        break;
      default:
        return ctx.reject();
    }

    ctx.accept();
  }).on('ready', function() {
    console.log('Client authenticated!');

    client.on('session', function(accept, reject) {
      var session = accept();
      session.once('exec', function(accept, reject, info) {
        console.log('Client wants to execute: ' + inspect(info.command));
        var stream = accept();
        stream.stderr.write('Oh no, the dreaded errors!\n');
        stream.write('Just kidding about the errors!\n');
        stream.exit(0);
        stream.end();
      });
    });
  }).on('end', function() {
    console.log('Client disconnected');
  });
}).listen(0, '127.0.0.1', function() {
  console.log('Listening on port ' + this.address().port);
});
```
