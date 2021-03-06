# liferay-microfrontends

### Creating your react-app 

you can use:

[create-react-app](https://github.com/facebook/create-react-app)

after creating your app, you should run the command beneath in your app root:

```
npm run eject
```

this will enable you to modify any kind of configuration files such as webpack.config ones
(this is very important for the purpose of this PoC)


we must have a webpack output config similar to this one:

```
module.exports = {
  devtool: 'eval',
  entry: './src/index.js',
  output: {
    filename: 'app.js',
    publicPath: '/',
    library: 'SimpleTodoListModule', -> This one must be unique for each ReactApp we want to put inside Liferay Portlets
    libraryTarget: 'umd',
    globalObject: 'this',
    umdNamedDefine: true
  }
}

```
at your *package.json* we need to create a task for generating our output (the whole application) in a single "*.js*" file :
```
"scripts" : {
  "build:webpack": "webpack --mode development && npm start",
}
```
by the configuration above, if our webserver are runing at *localhost:3000*
we should have access to the webpackBootstrap application code at: *localhost:3000/app.js*

### Liferay Portal

at Liferay Portal, we should deploy the *liferay/modules/external-portlet*

drag it to a page, then open the portlet configuration:

fit the *remote_app_bundle_src* input with your remote webpackBootstrap javascript code, served at localhost:3000/app.js
fit the *remote_app_html_selector* should be just an unique id
fit the *remote_app_module_name* must be exactly the same as configured at webpack.config in the output library parameter.

### Good to go

You should see at your Liferay Portal (after reloading the page) the React APP running smoothly.





