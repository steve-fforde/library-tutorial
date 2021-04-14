# Chapter 1: Setting up a babel outline

1. Open your terminal window (press `Ctrl + T`) 
2. Navigate to where you want to store your project (eg `cd ~/Documents`) 
3. Run the following commands n terminal 
	`$` denotes a new command prompt
	```
	$ mkdir library
	$ cd library
	$ mkdir src
	$ touch .babelrc .gitignore src/index.js
	$ npm init --force
	$ npm install --save-dev babel-cli babel-preset-env
	$ code .
	```
	> | Command | What it does... |
	> | --- | --- |
	> |  `cd <dir-name>` | moves into a directory |
	> | `code .` | open the current dir as a project in VS Code |
	> | `mkdir <dir-name>` | creates a directory |
	> | `npm init <option>` | creates your project config<br/>`--force` = use all the default options |
	> | `npm install <option> <package>` | installs a dependency<br/>`--save-dev` = used to compile but not to run your code.<br/>`babel-preset-env` = the package to install. |
	> | `touch <file-name-list>` | creates an empty file(s) |
	>
	> These instructions will create the following files:
	> ```  
	> <parent-folder>
	>   └─ library                << this is the project folder	
	>       ├─ node_modules       << dependencies are installed here
	>       │   └─ <dependencies> << never edit anything inside node_modules
	>       ├─ src                << your code goes here
	>       │   └─ index.js       << the main module
	>       ├─ .babelrc           << configuration of babel
	>       ├─ .gitignore         << configuration of git
	>       ├─ package-lock.json  << used by npm
	>       └─ package.json       << configuration of npm
	>```
	> **Warning:** Do not make any changes to any files in the `.\library\node_modules` folder nor the `.\library\package-lock.json` file, these are managed elsewhere.

4. Press ``Ctrl + ` `` to open the Terminal panel inside VS Code, you can use this instead of the separate terminal window.
5. Edit the `.\library\package.json` file, add a `start` property to the object `/scripts` object with the value `"./node_modules/.bin/babel-node ./src/"`
	> This provides a quick launch script called "Start" for our project.
	
6. Paste the following into `.\library\.babelrc` and save:
	``` json
	{
		"presets": ["env"]
	}
	```
	> This tells babel what settings to use, we are using the standard configuration which we installed earlier.
	
7. Paste the following into `.\library\.gitignore` and save:
	```
	node_modules/
	```
	> If you use git (now or later) this will tell it not to store your dependencies, as they will consume a lot of space!
	
8. Paste the following into `.\library\src\index.js` and save:
	``` js
	console.log(`
		Hello, World!
	`)
	
	```
	> This is the code that will run when you run.
	> We are using a template string over multiple lines to test that babel is working as this is advanced syntax
	
9. Run `npm start` in the terminal
	> Because of our `start` script in `.\library\package.json` this is the same as running `./node_modules/.bin/babel-node ./src/`.
	> You should see the response `Hello World!` with a blank line above and below.