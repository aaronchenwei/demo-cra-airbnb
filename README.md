# react-cra-airbnb

## Prerequisite

- node
- yarn
- Visual Studio Code (with following extenions)
  - Babel JavaScript
  - Theme - Oceanic Next
  - EditorConfig for VS Code
  - ESLint
  - Prettier - Code formatter

## Step 1 - to create a `demo` project with `create-react-app`

`create-react-app` could be installed globally through yarn. However, the frequency for using is relative lower than any other global commands.

`yarn` has support for using create-react-app without first installing the binary via

```shell
$ yarn create react-app demo
```

In such way, we don't need to remember to upgrade create-react-app before using it.

Actually `yarn create react-app demo` is equivalent to:

```shell
$ yarn global add create-react-app
$ create-react-app demo
```

Then we switch into `demo` directory

```shell
$ cd demo
```

## Step 2 - to generate `.editorconfig`

```
root = true

[*]
indent_style = space
indent_size = 2
end_of_line = lf
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true

[*.md]
trim_trailing_whitespace = false
```

## Step 3 - to add `prettier`

```shell
$ yarn add --dev husky prettier pretty-quick
```

To create a `prettier` configuration file `.prettierrc`:

```javascript
{
  "singleQuote": true,
  "trailingComma": "es5"
}
```

To create a file named `.prettierignore` that `prettier` could ignore processing. We could put `package.json` into ignore list.

And then patch `package.json`:

```patch
"scripts": {
+    "precommit": "pretty-quick --staged",
    "start": "react-scripts start",
```

Now `package.json` look like below.

```javascript
{

  "scripts": {
    "precommit": "pretty-quick --staged",
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test --env=jsdom",
    "eject": "react-scripts eject"
  }
}
```

We could format entire project using:

```shell
$ yarn pretty-quick
```

## Step 4 - to add `eslint` and `eslint-config-airbnb`

```shell
$ yarn add --dev eslint eslint-plugin-import eslint-plugin-react eslint-plugin-jsx-a11y eslint-config-airbnb
$ yarn add --dev babel-eslint eslint-plugin-prettier eslint-config-prettier
```

Create `.eslintrc.js`

```javascript
module.exports = {
  env: {
    browser: true,
    jest: true,
    es6: true,
    node: true,
  },
  extends: ['airbnb', 'prettier'],
  plugins: ['prettier'],
  rules: {
    'prettier/prettier': [
      'error',
      {
        singleQuote: true,
        trailingComma: 'es5',
      },
    ],
  },
  parser: 'babel-eslint',
  parserOptions: {
    ecmaFeatures: {
      jsx: true,
    },
  },
};
```

For file `src/registerServiceWorker.js`:

```patch
+ /* eslint-disable */
// In production, we register a service worker to serve assets from local cache.
```

To run eslint for existing code

```shell
$ yarn eslint --ext=js --ext=jsx --fix .
```

Modify `src/index.js`:

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import registerServiceWorker from './registerServiceWorker';

ReactDOM.render(React.createElement(App), document.getElementById('root'));
registerServiceWorker();
```

Rename `src/App.js` to `src/App.jsx` and modify:

```javascript
import React from 'react';
import logo from './logo.svg';
import './App.css';

const App = () => (
  <div className="App">
    <header className="App-header">
      <img src={logo} className="App-logo" alt="logo" />
      <h1 className="App-title">Welcome to React</h1>
    </header>
    <p className="App-intro">
      To get started, edit <code>src/App.js</code> and save to reload.
    </p>
  </div>
);

export default App;
```

Rename `src/App.test.js` to `src/App.test.jsx`
