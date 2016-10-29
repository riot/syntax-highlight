# Riot Syntax Highlighters

[Riot.js](http://riotjs.com/) tag syntax highlighting for 

* [Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=crisward.riot-tag)
* [Atom](https://atom.io/packages/riot-tag)
* [Sublime Text](https://packagecontrol.io/packages/Riot%20Tag)


![screencast](https://github.com/riot/syntax-highlight/raw/master/images/screen-cast.gif)

This extension supports HTML, Jade, Stylus and Coffeescript within script tags.

With this plugin you can use

```html
<yourtag>
  <script type="coffee">
    # your coffee script here
  </script>
  <script>
    // your javascript here
  </script>
</yourtag>
```
This will then have correct syntax highlighting.

### Jade / Pug Support

If you like white space sensitive languages, Jade can be
a very succinct way to write your tags. The compile process
converts all this to html before usage, so there are no
overheads to your packages tags. Riot-tag(Jade) supports
Jade syntax highlighting, along with embedded coffeescript,
stylus and normal JS.



```jade
yourtag
  p hello world

  script(type="coffee").
    # your coffee script here
    
  style.
    /* your css here */
    
  style(type="stylus")
    // your stylus here 

```

### Stylus Support

You can use stylus within your riot tags, the syntax highlighting requires you
to have the stylus syntax highlighting installed too. To compile stylus you'll
also need stylus included in your compile process (see browserify tip below). 

### Installation 

Visual Studio Code
```
cmd+shift+p
type: ext install riot-tag
```

Atom
```
cmd+shift+p
type: install package 
search for riot-tag, press enter, click install
```

Sublime Text
```
cmd+shift+p
type: install package 
search for riot-tag, select in drop down, press enter to click install
```


The package contains 2 syntax highlighters riot(html) and riot(jade). 
If your editor picks the wrong one, you can specify the correct one in your settings file for vscode and atom.
Sublime allows you use the `open all with current extension as` feature.


### Using with Browserify

If you like the idea of using Jade, Coffeescript, Stylus etc with your riot tags, adding the
below to your package.json file should get you most of the way. Just swap out the package names
if you'd prefer not to use any of the compile steps. Non of this is neccesary for riot, but it took
me a while to work this out when I started our with riot, once in place it can make a nice workflow.

```json
{
  "scripts":{
    "watch": "./node_modules/.bin/watchify src/app.coffee -v -o build/site.js",
    "build": "./node_modules/.bin/browserify src/app.coffee -d -p [minifyify --uglify [--mangle 0] --map build/app.map.json --output build/app.map.json] -o build/app.js"
  },
  "browserify": {
    "debug": true,
    "transform": [
      [
        "riotify",{
          "expr": false,
          "type": "coffee",
          "template": "jade"
        }
      ]
    ]
  },
  "devDependencies": {
    "riot": "^2.3.15",
    "riotify": "^0.1.2",
    "stylus": "^0.52.4",
    "browserify": "^11.2.0",
    "jade": "^1.11.0",
    "watchify": "^3.4.0",
    "minifyify": "^7.1.0"
  }
}
```
Then use `npm run watch` during development and `npm run build` prior to deployment for minified code.


### Giving Feedback

If you have any problems, feedback or just fancy starring this project
see https://github.com/riot/syntax-highlight


### History

|Version | Description
|----    |----
| 1.1.0  | Merged support for atom,sublime and vscode together. Move to riot organisation.
| 0.1.6  | Allows underscores in attribute names
| 0.1.5  | Can now use `style(type="stylus")`
| 0.1.4  | Fixed sourcename bug
| 0.1.1  | Can now use `script(type="coffee")` or `<script type="coffee">`
| 0.0.8  | Fixed Stylus Bug
| 0.0.7  | Added stylus support for Jade
| 0.0.6  | Allows multiple script tags in jade
