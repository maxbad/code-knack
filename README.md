# Code-Knack

A code evaluator on your web page. Support both client implements and server implements.

- Mobile compatibility
- Allow running code at client side or server (implement yourself)
- Inject required script files automatically
- Good design and theme support
- Syntax highlight editor (powered by [CodeMirror](http://codemirror.net/))
- Multi-languages support (powered by different projects, see table followed)

## Demo

![screen record](https://github.com/lyricat/code-knack/blob/master/docs/screenrecord.gif)

- [Simple Demo](https://lyricat.github.io/code-knack/demo)
- [Jeklly Demo](https://lyricat.github.io/code-knack-jekyll-demo/jekyll/update/2019/01/19/welcome-to-jekyll.html)
- [My Blog (Hexo)](https://lyric.im/code-knack)
- [GitPress.io](https://gitpress.io/c/12/languages)


## How to use

### For browser

1. use the production version in `/dist`

```html
<script src="./code-knack.min.js" type="application/javascript"></script>
```

2. CodeKnack uses [CodeMirror](http://codemirror.net/) as the editor, so you need to link CodeMirror's script and css files

```html
<link rel="stylesheet", href="./lib/codemirror/codemirror.css"></link>
<link rel="stylesheet", href="./lib/codemirror/theme/monokai.css"></link>
<script src="./lib/codemirror/codemirror.js" type="application/javascript"></script>
```

3. Configure CodeKnack and init.

if you use the default output of [marked](https://marked.js.org), you don't need to specify `elements` and `guessLang`. Or you need to find all elements contain code(usually in pre > code) and implement `guessLang`(a function uses an element as argument and return language name in lowercase)

```javascript
 var codeKnack = new CodeKnack({
    codeKnackPath: './lib/code-knack',  // the resource path of code-knack
    elements: elements,                 // an array contains elements with code
    guessLang: guessLang,               // a function to guess language in each element
    enabledLanguages: langs,            // enabled language array
    languages: {                        // language config
      'javascript': {                   
        mode: 'browser',                      // use browser based implement
        scripts: ['./lib/codemirror/mode/javascript/javascript.js'],    // required script
      },
      'scheme': {
          mode: 'browser',
          scripts: ['./lib/codemirror/mode/scheme/scheme.js', './lib/engines/biwascheme-min.js'],  // load biwascheme to enable scheme implement
      },
      'css': {
          mode: 'view',                 // mode == 'view', can not run.
          scripts: ['./lib/codemirror/mode/css/css.js'],
      },
      ...
    }
 })
 codeKnack.init()
```

See [Demo](https://github.com/lyricat/code-knack/tree/master/docs/demo) for more details.

### For npm package

WIP

## CodeKnack Options

| Options | Defaults | Description |
| --- | --- | --- |
| codeKnackPath | '/lib/code-knack/' | path to CodeKnack's resource |
| elements | will use the `pre > code` elements generated by [marked](https://marked.js.org/) package | an array contains elements with code |
| guessLang | will guess the language from `pre > code` elements generated by [marked](https://marked.js.org/) package | a function to guess language in each element |
| enabledLanguages| - | enabled language array |
| languages | - | see followed |

### CodeKnack Language Options

| Options | Defaults | Description |
| --- | --- | --- |
| mode | - | 'view', 'browser' or 'proxy' |
| proxyUrl| - | required option when mode == 'proxy'. A url to handle code |
| scripts | - | required option when mode == 'browser'. Scripts to run, CodeKnack injects them into HTML |

## Support Languages


| Language | Implement |
| --- | --- |
| C/CPP 	| [JSCPP](https://github.com/felixhao28/JSCPP) |
| javascript 	| - |
| python 2.7	| [Skulpt](skulpt.org) |
| ruby		| [Opal](https://opalrb.com/#) |
| scheme	| [Biwascheme](https://www.biwascheme.org) |
| swift		| [iSwift](https://iswift.org/) |


## Developement

install dependences.

```bash
$ npm install
```

build dev version

```bash
$ npm run dev
```


build production version

```bash
$ npm run prod
```
