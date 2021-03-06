---
title: Deploy Node.js Applications
---

This page will prepare you to deploy Node.js apps via the [getting started guide](../../../dotcom/getting-started.html).

## <a id='packagejson'></a> Application package file ##

Cloud Foundry expects a `package.json` in your Node.js application. You can specify the version of Node.js you want to use in the `engine` node of your `package.json` file. As of July, 2013, Cloud Foundry uses 0.10.x as the default.

Here is an example for your `package.json` file.
~~~JSON
{
  "name": "default-nodejs-app",
  "version": "0.0.1",
  "author": "Your Name",
  "dependencies": {
    "express": "3.4.8",
    "consolidate": "0.10.0",
    "express": "3.4.8",
    "swig": "1.3.2",
  },
  "engines": {
    "node": "0.10.x",
    "npm": "1.3.x"
  }
}
~~~

## <a id='start'></a> Application start command ##

Node.js applications require a start command, which is saved with other configurations in `manifest.yml`.

You will be asked if you want to save your configuration the first time you deploy. This will save a `manifest.yml` in your application with the settings you entered during the initial push. Edit the `manifest.yml` file and create a start command as follows:

~~~yaml
---
applications:
- name: my-app
  command: node my-app.js
... the rest of your settings  ...
~~~

Alternately, specify the `cf push -c` flag.

<pre class="termainl">
$ cf push -c "node my-app.js"
</pre>

## <a id='nodemodules'></a> Application bundling ##

You do not need to run `npm install` before deploying your application. Cloud Foundry will run it for you when your application is pushed. If you would prefer to run `npm install` and create a `node_modules` folder inside of your application, this is also supported.

## <a id='buildpack'></a> Node.js buildpack ##

If Cloud Foundry does not automatically detect that your application is a Node.js application, you can override the auto-detection by specifying the Node.js buildpack.

Either, add the buildpack into your `manifest.yml` and re-run `cf push -f`

~~~yaml
---
applications:
- name: my-app
  buildpack: https://github.com/cloudfoundry/heroku-buildpack-nodejs.git
... the rest of your settings  ...
~~~

Or, specify the `cf push -b` flag.

<pre class="termainl">
$ cf push -b https://github.com/cloudfoundry/heroku-buildpack-nodejs.git
</pre>

## <a id='services'></a> How do I bind services? ##

Refer to the [instructions for node.js service bindings](../../services/node-service-bindings.html).
