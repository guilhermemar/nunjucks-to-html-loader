# Nunjucks to HTML Loader for Webpack
Parse a template nunjucks to html string

* Accept `extend` and `include`
* Load relatives paths (doesn't use templates folder)
* Support alias folders
* Work with HtmlWebpackPlugin
* Work better twith html loader


## Installation

```bash
  $ npm install --save-dev nunjucks-to-html-loader
```

## Usage

### Webpack configuration

```javascript
module.exports = {
  ...
  module : {
    rules : [
      {
        test    : /\.(html?|njk)$/,
        exclude : /node_modules/,
        use     : [
            'html-loader',
            "nunjucks-to-html-loader"
        ]
      }
    ]
  }
  ...
};

```

### Options

#### Alias
For convenience is possible set alias for includes and extends path, you just set it in ths options:

```javascript
...
{
  test : /\.(html?|njk)$/,
  exclude : /node_modules/,
  use : [
      'html-loader',
      {
        loader  : "nunjucks-to-html-loader",
        options : {
          alias : {
            templates : path.resolve(__dirname, 'source/templates'),
            includes  : path.resolve(__dirname, 'source/templates/includes'),
            extends   : path.resolve(__dirname, 'source/templates/extends')
          }
        }
      }

  ]
}
...
```
And in template you need use `~` plus alias name. (like in css)

```nunjucks
  extend('~extends/some-base.html');
  or
  include('~includes/some-include.html');

```

#### Context
You can define a context json to use for all templates in the loader

```javascript
...
{
  test : /\.(html?|njk)$/,
  exclude : /node_modules/,
  use : [
      'html-loader',
      {
        loader  : "nunjucks-to-html-loader",
        options : {
          context : {
            valueA : 'Value A',
            valueB : {
              valueC : ['D', 'E', 'F']
            }
          }
        }
      }

  ]
}
...
```
