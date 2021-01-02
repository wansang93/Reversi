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
   ls  # package.join
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
            <label for='Enter your username' class='col-form-label sr-only'>Enter your username</label>
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

### Part 06 

