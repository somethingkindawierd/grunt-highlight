# grunt-highlight

> Run highlight.js over files

## Getting Started
This plugin requires Grunt.

If you haven't used [Grunt](http://gruntjs.com/) before, be sure to check out the [Getting Started](http://gruntjs.com/getting-started) guide, as it explains how to create a [Gruntfile](http://gruntjs.com/sample-gruntfile) as well as install and use Grunt plugins. Once you're familiar with that process, you may install this plugin with this command:

```shell
npm install grunt-highlight --save-dev
```

Once the plugin has been installed, it may be enabled inside your Gruntfile with this line of JavaScript:

```js
grunt.loadNpmTasks('grunt-highlight');
```

## The "highlight" task

### Overview
In your project's Gruntfile, add a section named `highlight` to the data object passed into `grunt.initConfig()`.

```js
grunt.initConfig({
  highlight: {
    task: {
      options: {
        // Task-specific options go here.
      },
      your_target: {
        // Target-specific file lists and/or options go here.
      }
    }
  }
});
```

### Options

#### options.lang
Type: `Boolean`
Default value: `false`

If you know the highlight language, use this.

#### options.useCheerio
Type: `Boolean`
Default value: `true`

You target files are HTML and you want to parse over them and highlight code blocks. *Turn off for raw code input*.

#### options.selector
Type: `Boolean`
Default value: `pre code`

This is what cheerio will be looking for as code block in your HTML. *Only used when useCheerio is true*.

### Usage Examples

#### Default Options

```js
grunt.initConfig({
  highlight: {
    task: {
      options: {},
      files: {
        'dest/out.html': ['src/in.html'],
      }
    }
  }
});
```

#### Full Code Files

If you want to highlight an entire file then use the following:

```js
grunt.initConfig({
  highlight: {
    task: {
      options: {
        useCheerio: false,
        lang: 'javascript' // treat the file as a javascript file
      },
      files: {
        'dest/highlighted.html': ['src/bunch-o-javascript.js'],
      }
    }
  }
});
```

#### One-to-One Compilation

Sometimes you want to take in a folder of code, and output a folder of highlighted HTML.

```js
highlight: {
  scripts: {
    options: {
      useCheerio: false, // these are pure js files
      lang: 'javascript' // there is no auto-detect for files
    },
    files: [{
      expand: true,
      cwd: 'scripts', // in folder
      src: ['{,*/}*.js'],
      dest: 'html', // out folder
      rename: function(dest, src) {
        // we dont want the output to be .js, make it .html
        return dest + '/' + src.replace(/\.js$/, '.html');
      }
    }]
  }
}
```

#### Many Tasks

```js
grunt.initConfig({
  highlight: {
    scripts: {
      options: {
        useCheerio: false,
        lang: 'javascript'
      },
      files: {
        'javascript.html': ['src/script.js']
      }
    },
    styles: {
      options: {
        useCheerio: false,
        lang: 'css'
      },
      files: {
        'stylesheet.html': ['src/style.css']
      }
    }
  }
});
```

## Contributing
In lieu of a formal styleguide, take care to maintain the existing coding style. Add unit tests for any new or changed functionality. Lint and test your code using [Grunt](http://gruntjs.com/).

## Release History
_(Nothing yet)_

## License
Copyright (c) 2013 James Doyle. Licensed under the MIT license.
