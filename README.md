driveshare-gui
==============
Cross platform desktop application meant to simplify usage of [dataserv-client](https://github.com/Storj/dataserv-client).

The application is built with web technologies (HTML / CSS / Javascript) using [Electron](http://electron.atom.io/).

This project began as a fork of [electron-boilerplate](https://github.com/szwacz/electron-boilerplate) by [szwacz](https://github.com/szwacz).

# Quick start
The only development dependency of this project is [Node.js](https://nodejs.org). So just make sure you have it installed.
Then type few commands known to every Node developer...
```
git clone https://github.com/Storj/driveshare-gui
cd driveshare-gui
npm install
npm start
```
... and boom! You have running desktop application on your screen.

# Structure of the project

There are **two** `package.json` files:  

#### 1. For development
Sits on path: `driveshare-gui/package.json`. Here you declare dependencies for your development environment and build scripts. **This file is not distributed with real application!**

Also here you declare the version of Electron runtime you want to use:
```json
"devDependencies": {
  "electron-prebuilt": "^0.24.0"
}
```

#### 2. For the application
Sits on path: `driveshare-gui/app/package.json`. This is **real** manifest of your application. Declare the app dependencies here.

### Project's folders

- `app` - code of your application goes here.
- `config` - place for you to declare environment specific stuff.
- `build` - in this folder lands built, runnable application.
- `releases` - ready for distribution installers will land here.
- `resources` - resources for particular operating system.
- `tasks` - build and development environment scripts.


# Development

#### Installation

```
npm install
```
It will also download Electron runtime, and install dependencies for second `package.json` file inside `app` folder.

#### Starting the app

```
npm start
```

#### Adding pure-js npm modules to your app

Remember to add your dependency to `app/package.json` file, so do:
```
cd app
npm install name_of_npm_module --save
```

#### Adding native npm modules to your app

If you want to install native module you need to compile it agains Electron, not Node.js you are firing in command line by typing `npm install` [(Read more)](https://github.com/atom/electron/blob/master/docs/tutorial/using-native-node-modules.md).
```
npm run app-install -- name_of_npm_module
```
Of course this method works also for pure-js modules, so you can use it all the time if you're able to remember such an ugly command.

#### Module loader

How about splitting your JavaScript code into modules? This project supports it by new ES6 syntax (thanks to [babel](https://babeljs.io/)). ES6 modules are translated into AMD (RequireJS) modules. The main advantage of this setup is that you can use ES6 -> RequireJS for your own modules, and at the same time have normal access to node's `require()` to obtain stuff from npm.
```javascript
// Modules you write are required through new ES6 syntax
// (It will be translated into AMD definition).
import myOwnModule from './my_own_module';
// Node.js (npm) modules are required the same way as always
// (so you can still access all the goodness of npm).
var moment = require('moment');
```

#### Unit tests

electron-boilerplate has preconfigured [jasmine](http://jasmine.github.io/2.0/introduction.html) unit test runner. To run it go with standard:
```
npm test
```
You don't have to declare paths to spec files in any particular place. The runner will search through the project for all `*.spec.js` files and include them automatically.


# Making a release

**Note:** There are various icon and bitmap files in `resources` directory. Those are used in installers and are intended to be replaced by your own graphics.

To make ready for distribution installer use command:
```
npm run release
```
It will start the packaging process for operating system you are running this command on. Ready for distribution file will be outputted to `releases` directory.

You can create Windows installer only when running on Windows, the same is true for Linux and OSX. So to generate all three installers you need all three operating systems.

# Install windows

After download the primary installer, the program will get the needed actual program parts.
This will take a short time (If the program does not continue downloading these parts for more than 2 minutes restart the installer) 
When succesfull the program opens the preferences page where you need to set the all important information to continue:
1) The counterwallet bitcoin address for the payout of your sjcx and holding the funds for optional donations.
2) Directory where you are going to save the data files (shards) needed for Storj.
3) The amount in G(iB)/GB and T(iB)/TB "officially iB = 1000 and B = 1024", Example for 10 GiB =  10.0G
4) Finish this by pushing the save (you can make changes anytime in preferences again.

## Special precautions for Windows
As installer [NSIS](http://nsis.sourceforge.net/Main_Page) is used. You have to install it (version 3.0), and add NSIS folder to PATH in Environment Variables, so it is reachable to scripts in this project (path should look something like `C:/Program Files (x86)/NSIS`).

## Freqeuntly Asked Questions

# Windows

1) Q: Install program does not continue after start and seems to hangup.  
   A: Close the program and start it again, if it still does not continue please report this as a issue here at github
   
   
# License

The MIT License (MIT)

Copyright (c) 2015 Jakub Szwacz

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
