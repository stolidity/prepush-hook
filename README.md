prepush-hook2
============

An npm installable git pre-push hook used to run npm scripts on pre-push.
Thanks to [nlf] and [marapper] for their work on [precommit-hook] and [prepush-hook]

The main difference between this and prepush-hook is that it does not force you to install jshint. You can install your own linter, such as eslint, or no linter at all. Simply define whatever scripts you want in your package.json and add them to the `prepush` array, and they will run. It makes no assumptions about your stack and what tools you use.

[nlf]:https://github.com/nlf
[precommit-hook]:https://github.com/nlf/precommit-hook
[marapper]:https://github.com/marapper
[prepush-hook]:https://github.com/marapper/prepush-hook

Installation
-----

    npm install prepush-hook2


Everything else is automatic!

I recommend putting prepush-hook2 in your project's devDependencies to make sure that anyone who may be contributing to your project will have the hook installed.

```
{
  "name": "your_project",
  "description": "just an example",
  "scripts": {
    "validate": "./command/to/run",
    "test": "./other/command"
  },
  "devDependencies": {
    "prepush-hook2": "latest"
  }
}
```

Usage
-----

```javascript
{
  "name": "your_project",
  "description": "just an example",
  "prepush": ["test"]
}
```

If you do not configure the hook with an array of scripts to run, it will default to `["validate", "test"]` to maintain backwards compatibility with the old version of this hook. 

Package.json
------------

```javascript
{
  "name": "your_project",
  "description": "just an example",
  "scripts": {
    "validate": "./command/to/run",
    "test": "./other/command"
  }
}
```

The contents of the validate and test properties are the shell command to be run to perform those functions. Having these specified in your package.json also
lends you the ability to be able to run them manually like so

```
npm run-script validate
npm test
```

These scripts can be any shell executable commands, but must exit with a status code of 0 for success and 1 or greater for failure. The `PATH` environment variable used when executing these scripts will be similar to how npm configures it. That means if you `npm install jshint` locally to your project, you can put simply `"jshint ."` for your script rather than `"./node_modules/.bin/jshint ."`.

You may configure what scripts will be run by the hook, by passing an array of script names to the `"prepush"` key in your package.json.

```javascript
{
  "name": "your_project",
  "description": "just an example",
  "scripts": {
    "lint": "jshint --with --different-options",
    "validate": "./command/to/run",
    "test": "./other/command"
  },
  "prepush": ["lint", "test"]
}
```

This example would run only the `lint` and `test` scripts, in that order.

License
-------

MIT
