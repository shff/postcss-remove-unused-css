# postcss-remove-unused-css

This is a simple to use PostCSS plugin that whitelists your CSS selectors based on your other files.

Unlike Uncss, the content doesn't matter: we're running a simple regex on the text files instead of a parser. We're also not running any Javascript. Therefore, it is simpler, but it might produce some false-positives.

It is inspired by PurifyCSS and works similarly.

## Installation:

```
npm install postcss-remove-unused-css
```

```
yarn add postcss-remove-unused-css
```

## Usage

```js
const remover = require('postcss-remove-unused-css');
postcss([remover(options)]);
```

See [PostCSS] docs for examples for your environment.

#### Options

| Name      | Type     | Description                | Default Value                                              |
| --------- | -------- | -------------------------- | ---------------------------------------------------------- |
| path      | `String` | Path to your project files | "./src"                                                    |
| exts      | `Array`  | Extensions to look into    | [".js", ".jsx", ".ts", ".tsx", ".html", ".vue", ".svelte"] |
| whitelist | `Array`  | Your whitelisted words     | ["html", "body"]                                           |

Always remember not to include CSS files in your extensions!

#### Using `.postcssrc`

```json
{
  "plugins": {
    "postcss-remove-unused": {
      "path": "./app",
      "exts": [".js", ".html"]
    }
  }
}
```

#### Using `package.json`:

```json
  "postcss": {
    "plugins": {
      "postcss-remove-unused": {
        "path": "./app",
        "exts": [".js", ".html"]
      }
    }
  },
```

### License

Copyright (c) 2019 Silvio Henrique Ferreira. See the LICENSE file for license rights and limitations (MIT).
