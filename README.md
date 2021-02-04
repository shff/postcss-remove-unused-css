# postcss-remove-unused-css

This is a simple to use PostCSS plugin that removes CSS selectors based on your other files.

This package is inspired by [PurifyCSS](https://github.com/purifycss/purifycss) and works the same way.

## How it works

It scans your HTML and JS files (you can configure which extensions it looks) and looks for words. Then it compares with words in your CSS selectors and filters out selectors without matches. If you have the word `blue` written in one of your JS or HTML files, it will allow a selector called `.blue` in your CSS. It is a simple and imperfect system, but it works.

Unlike [UnCSS](https://github.com/uncss/uncss), the content of your other files don't matter: we're running a simple regex match against the text files instead of a parser. We're also not running any Javascript. Therefore, it is simpler, but it might produce some false-positives. If you need a more precise approach we strongly recommend [UnCSS](https://github.com/uncss/uncss).

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

## Configuration Examples

#### Using `.postcssrc`

```json
{
  "plugins": {
    "postcss-remove-unused-css": {
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
      "postcss-remove-unused-css": {
        "path": "./app",
        "exts": [".js", ".html"]
      }
    }
  },
```

## Example

#### HTML File:

```html
<!DOCTYPE html>
<html>
  <body>
    <div class="blue bold">Hello, world!</div>
  </body>
</html>
```

#### Before

```css
body { background: gray }
.blue { color: blue }
.red { color: red }
.pink { color: pink }
.bold { font-weight: bold }
.thin { font-weight: 100 }
.center { text-align: center }
```

#### After

```css
body { background: gray }
.blue { color: blue }
.bold { font-weight: bold }
```

## Caveats

Don't include CSS files in the list of extensions in the options. This will make the plugin look for identifiers inside CSS files and the plugin won't optimize your code.

I'm using a simple file traversal algorithm instead of a Glob. I haven't tested it in all operating systems and environments, only the popular ones. Please file an issue and I'll look into it.

## License

Copyright (c) 2019-2021 Silvio Henrique Ferreira. See the LICENSE file for license rights and limitations (MIT).

```
MIT License

Copyright (c) 2019-2021 Silvio Henrique Ferreira

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
```
