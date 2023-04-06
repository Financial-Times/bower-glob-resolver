# ⚠️ Archived
As this library is no longer in use

# Bower Glob Resolver

[![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/Financial-Times/bower-glob-resolver/blob/main/LICENSE) [![Build Status](https://travis-ci.org/Financial-Times/bower-glob-resolver.svg?branch=main)](https://travis-ci.org/i-like-robots/bower-glob-resolver) [![npm version](https://img.shields.io/npm/v/bower-glob-resolver.svg?style=flat)](https://www.npmjs.com/package/bower-glob-resolver) [![Greenkeeper badge](https://badges.greenkeeper.io/i-like-robots/bower-glob-resolver.svg)](https://greenkeeper.io/)

A [resolver plugin] for [Bower] which enables the use of multiple `bower.json` files which are found using a [glob pattern]. This is useful for codebases which contain multiple packages or have dependencies which are not installed using Bower.

[resolver plugin]: https://bower.io/docs/pluggable-resolvers/
[Bower]: https://bower.io/
[glob pattern]: https://www.npmjs.com/package/glob#glob-primer


## Installation

This is a [Node.js] module available through the [npm] registry. Before installing, download and install Node.js. Node.js 8 or higher is required.

Installation is done using the [npm install] command:

```sh
$ npm install --save-dev bower-glob-resolver
```

After installing this package you will need create or amend Bower's `.bowerrc` [configuration file] to declare the newly installed resolver:

```diff
{
  "resolvers": [
+    "bower-glob-resolver"
  ]
}
```

[Node.js]: https://nodejs.org/en/
[npm]: https://www.npmjs.com/
[npm install]: https://docs.npmjs.com/getting-started/installing-npm-packages-locally
[configuration file]: https://bower.io/docs/config/


## Usage

This resolver will be used whenever a dependency's source begins with `glob:`. The value after this prefix must be a valid [glob pattern] ending with `bower.json`.

For example, a project containing multiple components may have this folder structure:

```
my-project/
├── components/
│   ├── footer/
│   │   └── bower.json
│   └── header/
│       └── bower.json
├── .bowerrc
└── bower.json
```

To install all of the Bower dependencies for every component in the project a new dependency must be added to the root `bower.json` file (the name doesn't matter so long as it is unique!) The source of this dependency should be a glob pattern matching the component's `bower.json`:

```json
{
  "dependencies": {
    "my-components": "glob:components/*/bower.json"
  }
}
```

When running `bower install` this resolver will log each extra `bower.json` file it finds and uses:

```bash
$ bower install
> bower my-components#*  glob-resolver Adding dependency on /my-project/components/footer/bower.json
> bower my-components#*  glob-resolver Adding dependency on /my-project/components/header/bower.json
```


## How it works

This resolver works by creating a temporary package which has dependencies on all of the packages matched by the glob pattern.


### License

This package is MIT licensed.
