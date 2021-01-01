# Reversi
This is a web application version of the game Reversi(aka. othello)

## Schedule

- 2021-01-01 Acquire a concept, Implement index.html, about.html, about links and name.html

## You can Enjoy here!

my web site -> [https://wansang93.herokuapp.com/](https://wansang93.herokuapp.com/)

## Reference

How to make Reversi -> [https://www.youtube.com/playlist?list=PLix7MmR3doRrOc1NaL18lwSjc1-2ecrgX](https://www.youtube.com/playlist?list=PLix7MmR3doRrOc1NaL18lwSjc1-2ecrgX)

Want to build like this site -> [https://dournac.org/info/othello#optimization](https://dournac.org/info/othello#optimization)

## TODO & Memo

웹 페이지가 유효한지 체크하는 사이트 링크 -> [https://validator.w3.org/](https://validator.w3.org/)

Copy script tag `soket.io` to connect server on the link -> [https://cdnjs.com/libraries/socket.io](https://cdnjs.com/libraries/socket.io)

## HOW TO BUILD

### Part 01

1. Design App
   - Download an application for moving pictures quickly on a mobile phone -> [marvelapp.com/pop](marvelapp.com/pop)

### Part 02

1. Download Node.js
   - Node.js Download link -> [https://nodejs.org/en/](https://nodejs.org/en/)

2. Download Howbrew
   - Package manager(only supported on masOS and Linux) Link -> [https://brew.sh/](https://brew.sh/)
   ```bash
   # install Homebrew(Homebrew is only supported on macOS and Linux.)
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   
   # check version
   node --version  # v14.15.3
   npm --version  # 6.14.9
   ```

3. Create a new Github repository
   - initialize gitignore file based on Node
   - Clone on my directory

4. go to command line on my directory
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

7. Make Directory and Imp
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

8. Push to GitHub -m `Here is the static file webserver`