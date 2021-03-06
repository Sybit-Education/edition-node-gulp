# Pattern Lab Node - Gulp Edition

The Gulp wrapper around [Pattern Lab Node Core](https://github.com/pattern-lab/patternlab-node) providing tasks to interact with the core library and move supporting frontend assets.

## Packaged Components

The Gulp Edition comes with the following components:

* `patternlab-node`: [GitHub](https://github.com/pattern-lab/patternlab-node), [npm](https://www.npmjs.com/package/patternlab-node)
* `patternengine-node-mustache`: [GitHub](https://github.com/pattern-lab/patternengine-node-mustache), [npm](https://www.npmjs.com/package/patternengine-node-mustache)
* `pattern-lab/styleguidekit-assets-default`: [GitHub](https://github.com/pattern-lab/styleguidekit-assets-default)
* `pattern-lab/styleguidekit-mustache-default`: [GitHub](https://github.com/pattern-lab/styleguidekit-mustache-default)

## Prerequisites

The Pattern Lab Node - Gulp Edition uses [Node](https://nodejs.org) for core processing, [npm](https://www.npmjs.com/) to manage project dependencies, and [gulp.js](http://gulpjs.com/) to run tasks and interface with the core library. Node version 4 or higher suffices. You can follow the directions for [installing Node](https://nodejs.org/en/download/) on the Node website if you haven't done so already. Installation of Node will include npm.

It's also highly recommended that you [install gulp](hhttps://github.com/gulpjs/gulp/blob/4.0/docs/getting-started.md) globally.

> Note: The Gulp Edition of Pattern Lab uses Gulp 4, which may require a new global install of the Gulp command line interface. Follow the [gulp upgrade instructions](https://github.com/pattern-lab/edition-node-gulp/wiki/Updating-to-Gulp-4) if you already have gulp installed and need to upgrade. Gulp 4 is in alpha, but brings many benefits to the table and is relatively stable. You can alternatively [run with local gulp instead of global gulp](https://github.com/pattern-lab/patternlab-node/wiki/Running-with-Local-Gulp-Instead-of-Global-Gulp), but commands are a bit more verbose. The rest of this documentation assumes a global install.

## Installing

There are two methods for downloading and installing the Gulp Edition:

* [Download a pre-built package](#download-a-pre-built-package)
* [Use npm](#use-npm)

### Download a pre-built package

The fastest way to get started with the Gulp Edition is to [download the pre-built version](https://github.com/pattern-lab/edition-node-gulp/releases) from the [releases page](https://github.com/pattern-lab/edition-node-gulp/releases). The pre-built project comes with the [Base Starterkit for Mustache](https://github.com/pattern-lab/starterkit-mustache-base) installed by default.

**Please note:** Pattern Lab Node uses [npm](https://www.npmjs.com/) to manage project dependencies. To upgrade the Gulp Edition or to install plug-ins you'll need to be familiar with npm.

### Use npm

`npm` is a dependency management and package system which can pull in all of the Gulp Edition's dependencies for you. To accomplish this:

* download or `git clone` this repository to an install location.

* run the following

    ```
    cd install/location
    npm install
    ```

Running `npm install` from a directory containing a `package.json` file will download all dependencies defined within.

#### Install the Gulp Edition of Pattern Lab Node as a Dependency

Most people want to run Pattern Lab Node standalone and not as a dependency. If you wish to install as a dependency you can do the following:

Use npm's [`install` command](https://docs.npmjs.com/cli/install) with an argument to install the Gulp Edition into a location of your choosing. In Terminal type:

    cd install/location/
    npm install edition-node-gulp

This will install the Gulp Edition into a directory called `node_modules` in `install/location/`.

## Getting Started

The Pattern Lab Node - Gulp Edition ships with a [base experience](https://github.com/pattern-lab/starterkit-mustache-base) which serves as clean place to start from scratch with Pattern Lab. But if you want to get rolling with a starterkit of your own, or use the [demo starterkit](https://github.com/pattern-lab/starterkit-mustache-demo) like the one on [demo.patternlab.io](http://demo.patternlab.io), you can do so automatically at time of `npm install` by adding your starterkit to the `package.json` file.

You can also [work with starterkits using the command line](https://github.com/pattern-lab/patternlab-node/wiki/Importing-Starterkits).

## Updating Pattern Lab

To update Pattern Lab please refer to each component's GitHub repository, and the [master instructions for core](https://github.com/pattern-lab/patternlab-node/wiki/Upgrading). The components are listed at the top of the README.

## Helpful Commands

These are some helpful commands you can use on the command line for working with Pattern Lab.

> Reminder: These commands assume a global installation of gulp 4.X, instead of a local installation. Depending on your preference, you may need to [upgrade your global version of gulp](https://github.com/pattern-lab/edition-node-gulp/wiki/Updating-to-Gulp-4) or [run with local gulp](https://github.com/pattern-lab/patternlab-node/wiki/Running-with-Local-Gulp-Instead-of-Global-Gulp).

### List all of the available commands

To list all available commands type:

    gulp patternlab:help

### Generate Pattern Lab

To generate the front-end for Pattern Lab type:

    gulp patternlab:build

### Watch for changes and re-generate Pattern Lab

To watch for changes, re-generate the front-end, and server it via a BrowserSync server,  type:

    gulp patternlab:serve

BrowserSync should open [http://localhost:3000](http://localhost:3000) in your browser.

### Install a StarterKit

To install a specific StarterKit from GitHub type:

    npm install [starterkit-vendor/starterkit-name]

    gulp patternlab:loadstarterkit --kit=[starterkit-name]
    
## E-Mail Templates

This module could be use for testing out the sending process of own email templates. Furthermore the stylesheet will be written inline.

### Define global and local configurations

Here are some pre-configurations you have to set up before sending the created email templates:

Create a new local configuration file in the project directory with the prefix **.local.json** and fill in the following elements with your personal email credentials: 

    "username": "xxx"
    "password": "xxx"

Update the global patternlab configuration file replacing the default values from file destinations, sources and relevant email informations.

    "authSrc": "./xxx.local.json"
    "styleSrc" : "./source/css/sass/**/*.sass"
    "styleDest" : "./source/css"
    "emailSrc" : "./public/patterns/05-emails/05-emails.rendered.html",
    "emailDest" : "./public/patterns/05-emails/"
    "host": "smtp.xxx.de",
    "port": 000
    "emailFrom": "xxx xxx <xxx@xxx.de>",
    "emailTo": "xxx@xxx.de",
    "emailSubject": "Test@E-Mail.Template"
    

### Run the build process

The command starts a series of several necessary jobs like generating the css file, the general building of the patterns and finally the inline-css job in the right order. Start the job-series with following command:

    gulp patternlab:build

### Sending the email template

After setting up the configurations and the build of the patterns the mail can be send out to your own mail account with the following command:

    gulp mail


### How does it work?


In the directory _./source/_meta/_ the file **_00-head.mustache** will be rendered in all html-files. With the variable **#email** the visibility of the stylesheet is managable.

	{{# email}}
	  <link rel="stylesheet" href="../../css/email.css?{{ cacheBuster }}" media="all" />
	{{/ email}}

Settings in the global **package.json**

   `"email": false`

Settings in the specific **email.json** (source folder of the email pattern)

   `"email": true`

