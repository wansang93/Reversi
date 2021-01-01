### Part 01 Design

1. Design App

   - Download an application for moving pictures quickly on a mobile phone -> [marvelapp.com/pop](marvelapp.com/pop)

### Part 02 Create the static file webserver

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
   npm install socket.io --save  # record that I need
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

   go to bootstrap then copy Starter template -> [link](https://getbootstrap.com/docs/5.0/getting-started/introduction/#starter-template)
   
   ```html
   <!doctype html>
   <html lang="en">
   <head>
      <!-- Required meta tags -->
      <meta charset="utf-8">
      <meta name="viewport" content="width=device-width, initial-scale=1">

      <!-- Bootstrap CSS -->
      <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-giJF6kkoqNQ00vy+HMDP7azOuL0xtbfIcaT9wjKHr8RbDVddVHyTfAAsrekwKmP1" crossorigin="anonymous">

      <title>Hello, world!</title>
   </head>
   <body>
      <h1>Hello, world!</h1>

      <!-- Optional JavaScript; choose one of the two! -->

      <!-- Option 1: Bootstrap Bundle with Popper -->
      <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta1/dist/js/bootstrap.bundle.min.js" integrity="sha384-ygbV9kiqUc6oa4msXn9868pTtWMgiQaeYH7/t7LECLbyPA2x65Kgf80OJFdroafW" crossorigin="anonymous"></script>

      <!-- Option 2: Separate Popper and Bootstrap JS -->
      <!--
      <script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.5.4/dist/umd/popper.min.js" integrity="sha384-q2kxQ16AaE6UbzuKqyBE9/u/KzioAlnx2maXQHiDX9d4/zp8Ok3f+M7DPm+Ib6IU" crossorigin="anonymous"></script>
      <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta1/dist/js/bootstrap.min.js" integrity="sha384-pQQkAEnwaBkjpqZ8RU1fF1AKtTcHJwFl3pblpTlHXybJjHpMYo79HY3hIi4NKxyj" crossorigin="anonymous"></script>
      -->
   </body>
   </html>
   ```

8. Push to GitHub -m `Create the static file webserver`

### Part 03 Implement index.html, about.html, wiki links and phototype name.html

1. Modify `index.html`
   
   in `<head>` tag
   ```html
    <title>Reversi</title>

    <style>
      body {
        background-image: url("assets/images/green.png");
      }
    </style>
   ```

   in `<body>` tag
   ```html
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
       <title>About</title>

    <style>
      #header-row {
        background-image: url("assets/images/green.png");
      }
    </style>

  </head>
  <body>
    <div class="container-fluid text-center">
      <div class="row", id="header-row">
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
   ```

### Part 04 