# WebGPU for Beginners 01: Node Package Manager

## Learning how to use Node package manager

Installing npm was a pain in the arse because I first had to uninstall the anaconda3 enviroment, which I had installed for univeristies physics lab module, which turned out not to be necessary for the very simply data analysis that we're doing in first year. Before uninstalling anaconda3 I installed brew, which was very simple. 
The problems started when trying to install nvm, because I had to learn how to use the basics of vim to edit the ./zshrc file. Once I figured that out it installed but it took around 30 minutes to figure out how. The next step was to find install npm using `nvm ls-remote` which returned `N/A` at first, after restarting the terminal `nvm ls-remote` worked. 
I installed the latest version using `nvm install 20.11.1`. 
In the code directory initialise npm using `npm init -y`, `-y` initialises npm with default values. This creates a new file called package.json inside the directory, which looks like this:
```
{
  "name": "npm-test",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```
Then use the command `npm i http-server`, which installs a bunch of dependencies, finally edit these values:
```
"scripts": {
    "start": "npm run install-dependencies && npm run serve",
    "install-dependencies": "npm i",
    "serve": "http-server"
  }
```
then use `npm start` in terminal to run server, which will return this:
```
> npm-test@1.0.0 start
> npm run install-dependencies && npm run serve


> npm-test@1.0.0 install-dependencies
> npm i


up to date, audited 47 packages in 574ms

15 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities

> npm-test@1.0.0 serve
> http-server

Starting up http-server, serving ./

http-server version: 14.1.1

http-server settings: 
CORS: disabled
Cache: 3600 seconds
Connection Timeout: 120 seconds
Directory Listings: visible
AutoIndex: visible
Serve GZIP Files: false
Serve Brotli Files: false
Default File Extension: none

Available on:
  http://127.0.0.1:8080
  http://192.168.1.172:8080
Hit CTRL-C to stop the server

[2024-03-10T21:31:31.486Z]  "GET /" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/122.0.0.0 Safari/537.36"
(node:58739) [DEP0066] DeprecationWarning: OutgoingMessage.prototype._headers is deprecated
(Use `node --trace-deprecation ...` to show where the warning was created)
[2024-03-10T21:31:31.553Z]  "GET /favicon.ico" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/122.0.0.0 Safari/537.36"
[2024-03-10T21:31:31.556Z]  "GET /favicon.ico" Error (404): "Not found"
^Chttp-server stopped.
```
Copy paste either of the `Available on:` addresses into web browser to access server, and hit `ctrl-c` to end server