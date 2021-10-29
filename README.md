# Meteor Git Packages

This tools helps you share private meteor packages.

## Getting Started

- `npm install -g @unparallel/mgp`

- Add `git-packages.json` to the root of your project.

````
{
  "my:private-package": {
    "git": "git@github.com:my/private-packages.git",
    "version": "commithashortag",
    "path": "optional/directory/path"
  },
  "my:other-private-package": {
    "git": "git@github.com:my/private-packages.git",
    "version": "commithashortag"
  },
  "my:yet-another-private-package": {
    "git": "git@github.com:my/private-packages.git",
    "branch": "dev"
  }
}
````

- Run `mgp` in your meteor directory to copy the packages from github or `mgp my:private-package` to copy an individual package.

You can also run `mgp --https` to convert github ssh urls to https. This is useful for using [`.netrc`](https://gist.github.com/jperl/91f32a37dc1c12c48ad8) on build machines.

- Add `local-packages.json` to the root of your project:

````
{
  "my:private-package": {
    "path": "~/path/to/private-package"
  },
  "my:other-private-package": {
    "path": "relative/path/to/other-private-package"
  }
}
````

- Run `mgp link` in your meteor directory to symlink your local packages or `mgp link my:private-package` to symlink an individual package.


- If you run `mgp --addToGlobals` the `addToGlobals` will run `meteor add` for each project fetched

## Add MGP to your project as a dev dependency

This sections explains how to add MGP as a dev dependency and how to run automatically after installing the npm dependencies, this is useful for CI/CD use cases 

* Install MGP as a dev dependency
 ````shell
npm install @unparallel/mgp --save-dev
 ````
* Update package.json to run mgp after npm install

````json

{
   "scripts": {
     "postinstall": "mgp --addToGlobals"
   }
}
````
* Now after running npm install, the meteor private packages defined on `git-packages.json` will be installed and added to meteor