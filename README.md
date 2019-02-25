# postcss-remove-unused-css

This is a simple to use PostCSS plugin that removes CSS selectors based on your other files.

It scans your HTML and JS files (the extensions are configurable) and looks for words. Then it compares with words in your CSS selectors and filters out selectors without matches. If you have the word `blue` written in one of your JS or HTML files, it will allow a selector called `.blue` in your CSS. It is a simple and imperfect system, but it works.

Unlike Uncss, the content of your other files doesn't matter: we're running a simple regex on the text files instead of a parser. We're also not running any Javascript. Therefore, it is simpler, but it might produce some false-positives.

It is inspired by PurifyCSS and works similarly.

## Caveats

I'm using a simple file traversal algorithm. I haven't tested it in all operating systems. Please file an issue and I'll look into it!

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

Always remember not to include CSS files in your extensions. This will make the plugin look for identifiers inside CSS files and the plugin won't optimize your code.

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

## License

Copyright (c) 2019 Silvio Henrique Ferreira. See the LICENSE file for license rights and limitations (MIT).
