A simple webapp example using NodeJS's Express.

Loosely following instructions at: https://developer.okta.com/blog/2018/11/15/node-express-typescript

Initialized with 
```
npm init
```

All the defaults were used when prompted to create the package.json

Install express with 
```
npm install express
```

Created `src/index.js` and updated `package.json`: changed `main` property and added a `start` script.

# Set up TypeScript

Run to install TypeScript compiler:
```
npm install --save-dev typescript  
```

Added `tsconfig.json` file. This can be autogenerated with:
```
npx tsc --init
```
Some settings made to match those listed here: https://developer.okta.com/blog/2018/11/15/node-express-typescript#set-up-your-nodejs-project-to-use-typescript

The TypeScript compiler will compile files in the `src` folder and place the results in the `dist` folder.

Added Typescript linting:
```
npm install --save-dev tslint
```

Added `tslint.json`. This can be autogenerated with:
```
npx tslint --init
```
Some settings are changed from the default.

Updated `package.json` to point main to the new `dist` folder, and with a few new scripts for prebuild, build, and prestart.

Changed `index.js` extension from `.js` to `.ts`.

Finally, run with:

```
npm run start
```

Note: You can run TSLint and the TypeScript compiler without starting the Node.js server using `npm run build`.

# TypeScript errors

Updated the `index.ts` to address some linter/compiler errors.

Update your project with some TypeScript declaration files so that TypeScript can use the type declarations for Node.js and Express.
```
npm install --save-dev @types/node @types/express
```

# Build a Better User Interface with Materialize and EJS

Adding Materialize and EJS.
Install EJS with:
```
npm install ejs
```

Add new folder in `src` called `views`, and a file called `index.ejs`.

Updated `index.ts` with code to use EJS as the view engine and render the index template for the home page.

Install more modules and TypeScript declarations needed to copy other types of files from src to dist:
```
npm install --save-dev ts-node shelljs fs-extra nodemon rimraf npm-run-all
npm install --save-dev @types/fs-extra @types/shelljs
```

Added a folder called `tools` and a new script called `copyAssets.ts`

## Update npm scripts

Update the scripts in `package.json`.

Finally, run with:

```
npm run dev
```


# Configuration Settings with Node.js

Instead of environment variables, use dotenv.

```
npm install dotenv
npm install --save-dev @types/dotenv
```

Create a `.env` file.

# Adding Authentication with Auth0

Auth0.com has a great free tier.

Create an Application for a "Regular Web Application", "Node.js (Express)", and "Integrate Now".

In the `Configure Auth0` section, simply update the port from 3000 to 8080 for configuring Auth0:
Allowed Callback URL should include http://localhost:8080/callback and use the default Allowed Logout URLs of http://localhost:8080.

Install express-openid-connect.
```
npm install express express-openid-connect --save
```
It seems TypeScript support for express-openid-connect is limited.

In the `Integrate the SDK` section, note the relevant information but do not copy the code.

A similar but nonidentical basic setup for integration is added in:
1. the new `src/middleware/sessionAuth.ts` file, 
2. the new lines in `src/index.ts`,
3. the new settings in `.env` using the relevant information.

Test the logging in process by going to the `localhost:8080/login` route. You should be redirected to Auth0's login box. After logging in, you should be redirected back to the homepage. 

You can log out by going to `localhost:8080/logout`, which also redirects back to the home page.

Check out both the `testauth` route and the `profile` route. The profile route will require you to login before accessing. The `testauth` will simply report on your logged in/out status.

Read more about usage of the `express-openid-connect` library here: https://github.com/auth0/express-openid-connect/blob/master/EXAMPLES.md#2-require-authentication-for-specific-routes

Note that to use Social Identity Providers (Facebook, Google, etc) in production, you will eventually need to register the app with the relevant Identity Provider to get a Client ID/Secret for the provider. Auth0 for now provides its own developer keys for convenience in development/testing.

## Refactor routes

A new view `stuff.ejs` is added.

New `src\routes\index.ts` moves all the routing code from `src/index.ts` into a separate place; a new auth-protected route for the `stuff` view is added. 




