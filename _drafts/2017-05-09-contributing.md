---
layout: post
title: Contributing to Cytoscape.js
subtitle: How to make your first contribution to Cytoscape.js
tags:
- tutorial
---

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Why Contribute?](#why-contribute)
- [Discussing Contributions](#discussing-contributions)
- [Making a contribution](#making-a-contribution)
  - [Forking and cloning](#forking-and-cloning)
  - [Making a new branch](#making-a-new-branch)
  - [Writing code](#writing-code)
    - [Style](#style)
    - [Committing](#committing)
    - [Code Organization](#code-organization)
    - [Building and Testing Cytoscape.js](#building-and-testing-cytoscapejs)
  - [Pushing changes](#pushing-changes)
  - [Creating a pull request and receiving feedback](#creating-a-pull-request-and-receiving-feedback)
- [Conclusion](#conclusion)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

[Cytoscape.js](https://js.cytoscape.org) is an open-source project and welcomes any and all contributions—everything from a small documentation fix to a significant new feature is appreciated.
It was created at the [Donnely Center](http://thedonnellycentre.utoronto.ca/) at the University of Toronto and is under active development, coordinated through [Github](https://github.com/cytoscape/cytoscape.js).

This guide is aimed primarily towards users without prior experience contributing to open-source software (OSS).
For contributors familiar with the process, the [`CONTRIBUTING.md`](https://github.com/cytoscape/cytoscape.js/blob/master/CONTRIBUTING.md) file is a good place to read about Cytoscape.js-specific guidelines, such as code style.

Before you get started with this guide, make sure [Node.js](https://nodejs.org/en/) is installed.
Any recent version should work.

## Why Contribute?

Cytoscape.js has a highly permissive [MIT License](https://github.com/cytoscape/cytoscape.js/blob/master/LICENSE), which allows users to modify the software as they see fit without requireing that they redistribute their changes.
However, contributing any changes back to the project are greatly appreciated, as this makes the software better for everyone.
Additionally, it means that your changes will be maintained as part of the project, making upgrading to newer versions of Cytoscape.js a lot easier—no more having to modify and rebuild the code for each release.
Plus, having your contributions in the main build of Cytoscape.js means you can take advantage of the various CDNs hosting builds of Cytoscape.js and save on bandwidth. 

## Discussing Contributions

Discussion for Cytoscape.js happens in a variety of places, among them [Stack Overflow](http://stackoverflow.com/questions/tagged/cytoscape.js), [Gitter](https://gitter.im/cytoscape/cytoscape.js), and GitHub [Issues](https://github.com/cytoscape/cytoscape.js/issues) and [Pull Request](https://github.com/cytoscape/cytoscape.js/pulls) pages.
For code contributions, most discussion will probably occur on the pull request (PR) for that contribution.
We ask that discussions 1) are kept civil and 2) are kept helpful.

## Making a contribution

Contributing can be broken down into a series of steps:
1. Fork the project
2. Clone your fork
3. Make a new branch
4. Make changes
5. Commit and push changes
6. Create a pull request
7. Keep track of requested changes, etc.

### Forking and cloning

Steps 1-2 [are covered in depth by GitHub](https://guides.github.com/activities/forking/).

In short, create a GitHub profile if you do not have one, [visit the GitHub page for Cytoscape.js](https://github.com/cytoscape/cytoscape.js), click the Fork button, and clone your fork to download the code to your computer (using either the GitHub Desktop client or the command line).

### Making a new branch

Once you have a copy of the code on your computer, you can create a new branch and start to work on your contribution(s).

> Branching is an important part of the Git workflow.
> In the case of Cytoscape.js, it allows development to proceed simultaneously on several branches such as `master` (which is the branch which official releases are based on), `unstable` (where new features are added), and various long-term development branches.

Cytoscape.js development happens on the `unstable` branch, so make sure you have this branch checked out before you create a new branch.
To checkout the branch, navigate to whichever directory you cloned Cytoscape.js to and run `git checkout unstable`.
Then, create your new branch (which will be based on the `unstable` branch) with `git checkout -b feature/awesomeThing` where `feature/awesomeThing` is a descriptive name for your contribution to Cytoscape.
`git checkout -b` will both create a new branch and checkout the new branch, so all changes to code following this command will affect your newly created branch while leaving other branches untouched.

If you are working with the Github Desktop client, follow [the GitHub guide](https://help.github.com/desktop/guides/contributing/creating-a-branch-for-your-work/), selecting the `unstable` branch to base your fork off of when prompted.

If you are contributing multiple new features to Cytoscape.js (or fixing multiple issues), create separate branches for each feature/ bugfix to make reviewing and merging changes easier.
Running `git checkout unstable` will restore the `unstable` branch where you can run `git checkout -b feature/anotherThing` to start a second branch and then run `git checkout feature/awesomeThing` and `git checkout feature/anotherThing` to switch between branches.

### Writing code

Once you've started a new branch, you can start to write code!
Although it's outside the scope of this guide; I'd recommend working in an editor such as [VSCode](https://code.visualstudio.com/), [Atom](https://atom.io/), or [Sublime Text](https://www.sublimetext.com/).
Cytoscape.js comes with a `.eslint.json` file which ESLint will use to inspect your code, helping to reduce bugs and maintain a uniform style.
Development of Cytoscape.js requires several additional packages which are defined in `package.json` including Gulp (build/ test/ formatting/ etc. automation), ESLint (formatting), and Mocha and Chai (tests and assertions), among others.
Install these by navigating to the folder containing Cytoscape.js and running `npm install`.

#### Style

On the topic of uniform style: the Cytoscape.js doesn't have a strict style guide.
The only rules are to use two spaces for indentation and use single-quotes around strings; other than this, just try to match the style of existing code.

Code can be automatically formatted by running `gulp format`; make sure that you've commited all changes before running this command so that formatting changes are kept separate from the underlying code changes.

#### Committing

As you write code, commit changes with `git add .` and `git commit -m "work on awesome feature"`.
If using GitHub Desktop, [review the guide from GitHub](https://help.github.com/desktop/guides/contributing/committing-and-reviewing-changes-to-your-project/) about commiting changes.

> Frequency of commits is a personal preference; however, I recommend commiting no more frequently than each "unit of work" where each unit is a block of changes to one or more files that do not break compilation of Cytoscape.js.

#### Code Organization

Important folders for development are described here:

- `src/`: The `src/` folder is likely where you'll spend most of your time; this folder contains the many files that are combined at build-time to create the `cytoscape.js` file that is used in applications.
- `test/`: The `test/` folder contains tests for Cytoscape.js. If you are contributing a feature that can be tested, please add tests for this feature. If you are contributing a bugfix, add a test that fails without your bugfix.
- `documentation/`: The `documentation/` folder contains documentation for all public features of Cytoscape.js (internal/ private APIs need not be documented here). For new features, please add documentation on how to use them here.
- `dist/`: The `dist/` folder contains the most recent publically-released version of Cytoscape.js. This is the version that is published to npm and [js.cytoscape.org/](http://js.cytoscape.org/) on each new release.
- `build/`: Building Cytoscape.js will compile the many files within `src/` and emit two files here: one containing a non-minified build of Cytoscape.js and one containing a minified build.

#### Building and Testing Cytoscape.js

To build and test new features or bugfixes, run `gulp build` (to build Cytoscape.js without testing) or `gulp test` (to run all tests).
If these commands fail, make sure `gulp-cli` is installed globally with `npm install -g gulp-cli` and that all dependencies of Cytoscape.js have been installed by running `npm install` in the root of the Cytoscape.js directory.

### Pushing changes

TODO

### Creating a pull request and receiving feedback

TODO

## Conclusion

TODO