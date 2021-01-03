# How to build

### Part 01 Design

1. Design App

   - Download an application for moving pictures quickly on a mobile phone -> [marvelapp.com/pop](marvelapp.com/pop)

### Part 02 Create `the static file webserver`

1. Download `Node.js`
   
   - Node.js Download link -> [https://nodejs.org/en/](https://nodejs.org/en/)

2. Download `Howbrew`
   
   - Package manager(only supported on masOS and Linux) Link -> [https://brew.sh/](https://brew.sh/)
   ```bash
   # install Homebrew(Homebrew is only supported on macOS and Linux.)
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   
   # check version
   node --version  # v14.15.3
   npm --version  # 6.14.9
   ```

3. Create a new `Github repository`
   
   - initialize gitignore file based on Node
   - Clone on my directory

4. Initialize node
   
   Go to command line on my directory
   ```bash
   npm init  # set up basic structure
       (reversi)
       (1.0.0)
       This is the game of reversi
       (index.js) server.js
       -
       (https://github.com/wansang93/reversi.git)
       keywords: reversi
       author: wansang kim
       license: (ISC) GPL-3.0
       (yes)
   ls  # package.json
   npm install socket.io@2.0.1 --save  # (--save) records that I need
   npm install node-static --save
   # found 4 vulnerabilities (3 low, 1 high)
   # run `npm audit fix` to fix them, or `npm audit` for details
   touch Procfile  # another set up file
   ```

5. Create a new application on HEROKU and Connect to GitHub
   
   Link -> [https://dashboard.heroku.com/new-app](https://dashboard.heroku.com/new-app)

   Automatic deploys -> Enable

6. Set up `server.js`
   
   ```javascript
   /* Include the static file webserver library */
   var static = require('node-static');

   /* Include the http server library */
   var http = require('http');

   /* Assume that we are running on Heroku */
   var port = process.env.PORT;
   var directory = __dirname + '/public';

   /* If we aren't on Heroku, then we need to readjust the port and directory
   * information and we know that because port won't be set */
   if(typeof port == 'undefined' || !port){
      directory = './public';
      port = 8080;
   }

   /* Set up a static web-server that will deliver files from the filesystem */
   var file = new static.Server(directory);

   /* Construct an http server that gets files from the file server*/
   var app = http.createServer(
         function(request, response){
               request.addListener('end',
                  function(){
                     file.serve(request, response);
                  }
               ).resume();
         }
      ).listen(port);

   console.log('The Server is running');
   ```

7. Make Directory and Implement `index.html`
   ```bash
   mkdir public
   cd public
   touch index.html
   ```

   go to bootstrap then copy Starter template -> [link](https://getbootstrap.com/docs/4.0/getting-started/introduction/#starter-template)

8. Push to GitHub -m `Create the static file webserver`

### Part 03 Implement `index.html`, `about.html`, wiki links and prototype `name.html`

1. Modify `index.html`

   ```html
    <title>Reversi Home</title>

    <style>
      body {
        background-image: url("assets/images/green.png");
      }
    </style>

    <div class="container-fluid text-center">
      <div class="row">
        <div class="col">
          <img class="img-fluid" src="assets/images/top-splash.jpg" alt="Rersi logo"/>
        </div>
      </div>
      <div class="row">
        <div class="col">
          <a href="name.html" class="btn btn-lg btn-secondary">Let's play</a>
        </div>
      </div>
      <div class="row">
        <div class="col">
          <img class="img-fluid" src="assets/images/bottom-splash.jpg" alt="Rersi logo 2"/>
        </div>
      </div>
      <div class="row">
        <div class="col">
          <a href="about.html" class="btn btn-lg btn-secondary">About</a>
        </div>
        <div class="col">
          <a href="https://namu.wiki/w/%EC%98%A4%EB%8D%B8%EB%A1%9C" class="btn btn-lg btn-info">Rules</a>
        </div>
      </div>
    </div>
    ```

2. Copy `index.html` into `about.html`, `name.html`

   ```bash
   cp index.html about.html
   cp index.html name.html
   ```

   `about.html`
   ```html
   <!doctype html>
   <html lang="en">

   <head>
   <!-- Required meta tags -->
   <meta charset="utf-8">
   <meta name="viewport" content="width=device-width, initial-scale=1">

   <!-- Bootstrap CSS -->
   <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/css/bootstrap.min.css"
      integrity="sha384-9aIt2nRpC12Uk9gS9baDl411NQApFmC26EwAOH8WgZl5MYYxFfc+NcPb1dKGj7Sk" crossorigin="anonymous">

   <title>About</title>

   <style>
      #header-row {
         background-image: url("assets/images/green.png");
      }
   </style>

   </head>

   <body>
   <div class="container-fluid text-center">
      <div class="row" , id="header-row">
         <div class="col">
         <h2>About</h2>
         </div>
      </div>
      <div class="row">
         <div class="col">
         <p>Lorum ipsum</p>
         </div>
      </div>
      <div class="row">
         <div class="col">
         <a href="index.html" class="btn btn-lg btn-secondary">Home</a>
         </div>
         <div class="col">
         <a href="https://namu.wiki/w/%EC%98%A4%EB%8D%B8%EB%A1%9C" class="btn btn-lg btn-info">Rules</a>
         </div>
      </div>
   </div>

   <!-- jQuery first, then Popper.js, then Bootstrap JS -->
   <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js"
      integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj"
      crossorigin="anonymous"></script>
   <script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.0/dist/umd/popper.min.js"
      integrity="sha384-Q6E9RHvbIyZFJoft+2mJbHaEWldlvI9IOYy5n3zV9zzTtmI3UksdQRVvoxMfooAo"
      crossorigin="anonymous"></script>
   <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/js/bootstrap.min.js"
      integrity="sha384-OgVRvuATP1z7JjHLkuOU7Xw704+h835Lr+6QL9UvYjZE3Ipu6Tp75j7Bh/kR0JKI"
      crossorigin="anonymous"></script>

   </body>

   </html>
   ```

### Part 04 Chat Overview

### Part 05 Update `name.html`

```html
<!doctype html>
<html lang="en">

<head>
  <!-- Required meta tags -->
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">

  <title>Enter your user name for Reversi</title>

  <style>
    #header-row {
      background-image: url("assets/images/green.png");
    }
  </style>

  <script>
    function submitForm() {
      var username = $('#username').val();
      window.location.href = 'lobby.html?username=' + username;
    }
  </script>

  <!-- Bootstrap CSS -->
  <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/css/bootstrap.min.css"
    integrity="sha384-9aIt2nRpC12Uk9gS9baDl411NQApFmC26EwAOH8WgZl5MYYxFfc+NcPb1dKGj7Sk" crossorigin="anonymous">

</head>

<body>
  <div class="container-fluid text-center">
    <div class="row" id="header-row">
      <div class="col">
        <h2>Enter Your User Name</h2>
      </div>
    </div>
    <div class='row'>
      <div class='col'>
        <form onsubmit='submitForm(); return false;' class='form-inline'>
          <div class='form-group'>
            <label for='username' class='col-form-label sr-only'>Enter your user name</label>
            <input class='form-control' type='text' value='' id='username' placeholder="Enter your user name" />
          </div>
          <button type='submit' class='btn btn-primary'>Done</button>
        </form>
      </div>
    </div>
  </div>

  <!-- jQuery first, then Popper.js, then Bootstrap JS -->
  <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js"
    integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj"
    crossorigin="anonymous"></script>
  <script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.0/dist/umd/popper.min.js"
    integrity="sha384-Q6E9RHvbIyZFJoft+2mJbHaEWldlvI9IOYy5n3zV9zzTtmI3UksdQRVvoxMfooAo"
    crossorigin="anonymous"></script>
  <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/js/bootstrap.min.js"
    integrity="sha384-OgVRvuATP1z7JjHLkuOU7Xw704+h835Lr+6QL9UvYjZE3Ipu6Tp75j7Bh/kR0JKI"
    crossorigin="anonymous"></script>

</body>

</html>
```

### Part 06 Chat Receiving URL Parameters

```bash
cp name.html lobby.html
mkdir js
cd js/
touch main.js
```

`lobby.html`
```html
<!doctype html>
<html lang="en">

<head>
  <!-- Required meta tags -->
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">

  <title>Reversi Game Lobby</title>

  <style>
    #header-row {
      background-image: url("assets/images/green.png");
    }
  </style>

  <!-- Bootstrap CSS -->
  <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/css/bootstrap.min.css"
    integrity="sha384-9aIt2nRpC12Uk9gS9baDl411NQApFmC26EwAOH8WgZl5MYYxFfc+NcPb1dKGj7Sk" crossorigin="anonymous">

</head>

<body>
  <div class="container-fluid text-center">
    <div class="row" id="header-row">
      <div class="col">
        <h2>Lobby</h2>
      </div>
    </div>
    <div class='row'>
      <div class='col'>
        <h3>Messages</h3>
        <div id='messages'>
        </div>
      </div>
    </div>
  </div>

  <!-- jQuery first, then Popper.js, then Bootstrap JS -->
  <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js"
    integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj"
    crossorigin="anonymous"></script>
  <script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.0/dist/umd/popper.min.js"
    integrity="sha384-Q6E9RHvbIyZFJoft+2mJbHaEWldlvI9IOYy5n3zV9zzTtmI3UksdQRVvoxMfooAo"
    crossorigin="anonymous"></script>
  <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/js/bootstrap.min.js"
    integrity="sha384-OgVRvuATP1z7JjHLkuOU7Xw704+h835Lr+6QL9UvYjZE3Ipu6Tp75j7Bh/kR0JKI"
    crossorigin="anonymous"></script>
  <script src='js/main.js'></script>
</body>

</html>
```

`js/main.js`

```javascript
/* functions for general use */

/* This function returns the value associated with 'whichParam' on the URL */
function getURLParameters(whichParam) {
    var pageURL = window.location.search.substring(1);
    var pageURLVariables = pageURL.split('&');
    for (var i = 0; i < pageURLVariables.length; i++) {
        var parameterName = pageURLVariables[i].split('=');
        if (parameterName[0] == whichParam) {
            return parameterName[1];
        }
    }
}

var username = getURLParameters('username');
if ('undefined' == typeof username || !username) {
    username = 'Anonymous_' + Math.random();
}

$('#messages').append('<h4>' + username + '</h4>');
```

### Part 07 Chat Connections

server socket <-> client socket have to communicate

Copy Script Tag at link -> [https://cdnjs.com/libraries/socket.io/2.3.0](https://cdnjs.com/libraries/socket.io/2.3.0)  
-> Paste on `lobby.html` for client

`main.js`

```javascript
/* Connect to the socket server */
var socket = io.connect();

socket.on('log', function (array) {
    console.log.apply(console, array);
});
```

`server.js`

```javascript
/*********************************************/
/*       Set up the web socket server        */
var io = require('socket.io').listen(app);

io.sockets.on('connection', function (socket) {
    function log() {
        var array = ['*** Server Log Message: '];
        for (var i = 0; i < arguments.length; i++) {
            array.push(arguments[i]);
            console.log(arguments[i]);
        }
        socket.emit('log', array);
        socket.broadcast.emit('log', array);
    }
    log('A web site connected to the server');

    socket.on('disconnect', function (socket) {
        log('A web site disconnected from the server');
    });
});
```

### Part 08 Chat First Message

`main.js`

```javascript
var chat_room = 'One_Room';

socket.on('join_room_response', function (payload) {
    if (payload.result == 'fail') {
        alert(payload.message);
        return;
    }
    $('#messages').append('<p>New user joined the room: <b>' + payload.username + '</b></p>');
});
```

`server.js`

```javascript
/* join_room command */
/* payload:
    {
        'room: room to join,
        'username': username of person joining
    }
    join_room_response:
    {
        'result': 'success',
        'room': room joined,
        'username': username that joined,
        'membership': number of people in the room including the new one
    }
    or
    {
        'result': 'fail',
        'message': failure message,
    }
*/
socket.on('join_room', function (payload) {
    log('server received a command', 'join_room', payload);
    if (('undefined' === typeof payload) || !payload) {
        var error_message = 'join_room had no payload, command aborted';
        log(error_message);
        socket.emit('join_room_response', {
            result: 'fail',
            message: error_message
        });
        return;
    }

    var room = payload.room;
    if (('undefined' === typeof room) || !room) {
        var error_message = 'join_room didn\'t specify a room, command aborted';
        log(error_message);
        socket.emit('join_room_response', {
            result: 'fail',
            message: error_message
        });
        return;
    }

    var username = payload.username;
    if (('undefined' === typeof username) || !username) {
        var error_message = 'join_room didn\'t specify a username, command aborted';
        log(error_message);
        socket.emit('join_room_response', {
            result: 'fail',
            message: error_message
        });
        return;
    }

    socket.join(room);
    var roomObject = io.sockets.adapter.rooms[room];
    if (('undefined' === typeof roomObject) || !roomObject) {
        var error_message = 'join_room couldn\'t create a room(internal error), command aborted';
        log(error_message);
        socket.emit('join_room_response', {
            result: 'fail',
            message: error_message
        });
        return;
    }

    var numClients = roomObject.length;
    var success_data = {
        result: 'success',
        room: room,
        username: username,
        membership: (numClients + 1)
    }

    io.sockets.in(room).emit('join_room_response', success_data);
    log('Room' + room + ' was just joined by ' + username);
});
```

### Part 09 Chat Second Message (v2)

`lobby.html`

```html
    <div class='row'>
      <div class='col'>
        <form onsubmit='send_message(); return false;'>
          <div class='form-group'>
            <label for='send_message_holder' class='col-form-label sr-only'>Enter your chat message</label>
            <input class='form-control' type='text' value='' id='send_message_holder'
              placeholder='Enter your chat message'/>
          </div>
          <button type='submit' class='btn btn-primary'>Send</button>
        </form>
      </div>
    </div>
```

`main.js`

```javascript
socket.on('send_message_response', function (payload) {
    if (payload.result == 'fail') {
        alert(payload.message);
        return;
    }
    $('#messages').append('<p><b>' + payload.username + ' says:</b> ' + payload.message + '</p>');
});

function send_message() {
    var payload = {};
    payload.room = chat_room;
    payload.username = username;
    payload.message = $('#send_message_holder').val();
    console.log('*** Client Log Message: \'send_message\' payload: ' + JSON.stringify(payload));
    socket.emit('send_message', payload);
}
```

`server.js`

```javascript
/* send_message command */
/* payload:
    {
        'room: room to join,
        'username': username of person sending the message,
        'message': the message to send
    }
    send_message_response:
    {
        'result': 'success',
        'room': room joined,
        'username': username of the person that spoke,
        'message': the message spoken
    }
    or
    {
        'result': 'fail',
        'message': failure message,
    }
*/
socket.on('send_message', function (payload) {
    log('server received a command', 'send_message', payload);
    if (('undefined' === typeof payload) || !payload) {
        var error_message = 'send_message had no payload, command aborted';
        log(error_message);
        socket.emit('send_message_response', {
            result: 'fail',
            message: error_message
        });
        return;
    }

    var room = payload.room;
    if (('undefined' === typeof room) || !room) {
        var error_message = 'send_message didn\'t specify a room, command aborted';
        log(error_message);
        socket.emit('send_message_response', {
            result: 'fail',
            message: error_message
        });
        return;
    }

    var username = payload.username;
    if (('undefined' === typeof username) || !username) {
        var error_message = 'send_message didn\'t specify a username, command aborted';
        log(error_message);
        socket.emit('send_message_response', {
            result: 'fail',
            message: error_message
        });
        return;
    }

    var message = payload.message;
    if (('undefined' === typeof message) || !message) {
        var error_message = 'send_message didn\'t specify a message, command aborted';
        log(error_message);
        socket.emit('send_message_response', {
            result: 'fail',
            message: error_message
        });
        return;
    }

    var success_data = {
        result: 'success',
        room: room,
        username: username,
        message: message
    }
    io.sockets.in(room).emit('send_message_response', success_data);
    log('Message sent to room ' + room + ' by ' + username);
});
```

### Part 10 Lobby - Architecture

### Part 11 Lobby - Setup 01

copy minified(jquery-3.5.1.min.js) at the link -> [https://code.jquery.com/](https://code.jquery.com/)

