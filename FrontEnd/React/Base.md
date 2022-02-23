Node is a runtime. The npm command line utility runs on the Node.js runtime.

[about-npm](https://docs.npmjs.com/about-npm)

**We strongly recommend using a Node version manager like nvm to install Node.js and npm.**

[downloading-and-installing-node-js-and-npm](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm)

`npm --version`

`node --version`

The public npm registry is a database of JavaScript packages, each comprised of software and metadata. 

The npm registry contains packages, many of which are also Node modules, or contain Node modules.

## About packages

A package is a file or directory that is described by a package.json file. A package must contain a package.json file in order to be published to the npm registry. 

### About package formats
A package is any of the following:
* a) A folder containing a program described by a package.json file.
* b) A gzipped tarball containing (a).
* c) A URL that resolves to (b).
* d) A <name>@<version> that is published on the registry with (c).
* e) A <name>@<tag> that points to (d).
* f) A <name> that has a latest tag satisfying (e).
* g) A git url that, when cloned, results in (a).

## About modules

A module is any file or directory in the node_modules directory that can be loaded by the Node.js require() function.

Note: Since modules are not required to have a 

`package.json` 

file, not all modules are packages. Only modules that have a

`package.json`

file are also packages.

In the context of a Node program, the module is also the thing that was loaded from a file. For example, in the following program:

    var req = require('request')

we might say that "The variable req refers to the request module".

## About scopes

A scope allows you to create a package with the same name as a package created by another user or organization without conflict.


