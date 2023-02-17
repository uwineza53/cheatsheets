# Modules
ES 6 Modules manual documentation, modules is new ES6 feature prior to commonjs modular system. Let see some of its features

## How to create and export modules
As example, let create a module named module.js and export some of its dependencies named or default.

```javascript
    export const arr = [1, 2, 3, 4, 5];
    export const greetings = (user) => console.log(`Hello ${user}`);
    const user = "Jonas Smith";

    export {user}

    export default function loguser(user) {
        console.log(`welcome ${user}`)
    }
```

## How to import module
To import named export wrapped in braces but with default export no braces and any name maybe used.
Note: module should have single default export

```javascript
    import logUser, { arr, greetings, user } from "./module.js";

    greetings('Jonas');
    logUser(user);
    console.log(arr);
```

## How to inject script into HTML
To add script to HTML you have to add type equal to module

```html
    <script type="module" scr="./index.js"> </script>
```

#### Note: For best code practice module should perform only one function

------------------------------------- Part 1 ----------------------------------------

# Parcing and bundling your project
As your is made of different modules, you are required to parce it for development and bundle it up for production.
This is command based section, let write sripts.

```bash
    npm init
    npm install parcel --save-dev
```

To start your developement with parcel, just do:
```bash
    npx parcel index.html
```

To avoid full project reload with, add hot module condition to the end of index.js
```javascript
    if(module.hot)
        module.hot.accept();
```

