### Instructions for React Project

#### in terminal

* mkdir folder-in-this-way
* mkdir src
* touch src/index.jsx and paste
(
      import React from 'react';
      import ReactDOM from 'react-dom';
      import App from './components/App';
      import { AppContainer } from 'react-hot-loader';

      const render = (Component) => {
        ReactDOM.render(
          <AppContainer>
            <Component/>
          </AppContainer>,
          document.getElementById('react-app-root')
        );
      };

      render(App);

      if (module.hot) {
        module.hot.accept('./components/App', () => {
          render(App)
        });
      }
)

* apm install react@0.16.2 (//install the Atom React package)
* npm init (nitialize npm by navigating to our directory, press enter after)
* touch .gitignore and paste
(.DS_STORE
node_modules
build)
* npm install react@15.5.4 react-dom@15.5.4 --save (begin installing dependencies)
* npm install webpack@3.4.0 --save-dev (install Webpack, make sure to install this specific version)
* npm install webpack@3.4.0 -g (install Webpack globally. This provides access to Webpack commands in the Terminal)

* npm install babel-core@6.24.1 babel-loader@7.0.0 babel-preset-es2015@6.24.1 babel-preset-react@6.24.1 --save-dev (use Babel to transpile our JSX into ES5 the browser understands)

* touch webpack.config.js and paste, revise title in plugins
(
      const webpack = require('webpack');
      const { resolve } = require('path');
      const HtmlWebpackPlugin = require('html-webpack-plugin');

      module.exports = {

        entry: [
          'react-hot-loader/patch',
          'webpack-dev-server/client?http://localhost:8080',
          'webpack/hot/only-dev-server',
          resolve(__dirname, "src", "index.jsx")
        ],

        output: {
          filename: 'app.bundle.js',
          path: resolve(__dirname, 'build'),
          publicPath: '/'
        },

        resolve: {
          extensions: ['.js', '.jsx']
        },

        devtool: '#source-map',

        devServer: {
          hot: true,
          contentBase: resolve(__dirname, 'build'),
          publicPath: '/'
        },

        module: {
          rules: [
            {
              test: /\.jsx?$/,
              loader: "babel-loader",
              exclude: /node_modules/,
              options: {
                presets: [
                  ["es2015", {"modules": false}],
                  "react",
                ],
                plugins: [
                  "react-hot-loader/babel"
                ]
              }
            }
          ]
        },

        plugins: [
          new webpack.HotModuleReplacementPlugin(),
          new webpack.NamedModulesPlugin(),
          new HtmlWebpackPlugin({
            template:'template.ejs',
            appMountId: 'react-app-root',
            title: 'React Help Queue',
            filename: resolve(__dirname, "build", "index.html"),
          }),
        ]
      };

)
* webpack
* mkdir src/components and touch src/components/App.jsx and paste
(
        import React from "react";
        import Header from "./Header";
        import TicketList from "./TicketList";


        function App(){
          return (
            <div>
              <Header/>
              <TicketList/>
            </div>
          );
        }

        export default App;

  )

* touch src/components/Header.jsx and paste template as below;
(
  import React from "react";

function Header(){
  return (
    <h1>Help Queue</h1>
  );
}

export default Header;
  )
* touch other components follow previous section
* npm install prop-types@15.5.10 --save (React components accept properties (known as props), setup) add below line on top of each Component
(import PropTypes from "prop-types";)

* npm install webpack-dev-server@2.5.0 -g
* npm install webpack-dev-server@2.5.0 --save-dev (add a development server. Like most tools we've used, the Webpack development server is an npm package. We'll install it both into our project's development environment, and globally)

We can now bundle and serve projects with the following two commands:
* webpack
* webpack-dev-server

* npm install react-hot-loader@3.0.0-beta.7 --save-dev (install a package called React-Hot-Loader specifically meant to work with Webpack-Dev-Server)

* npm install html-webpack-plugin@2.29.0 --save-dev (install a dependency called html-webpack-plugin)

* touch template.ejs and paste:
          <!DOCTYPE html>
          <head>
          <meta charset="utf-8">
          <title><%= htmlWebpackPlugin.options.title %></title>
          </head>
          <body>
          <% if (htmlWebpackPlugin.options.appMountId) { %>
          <div id="<%= htmlWebpackPlugin.options.appMountId%>"></div>
          <% } %>
          </body>
          </html>

* delete index.html

* npm run test

* add the following to package.json:
        "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1",
        "start":  "webpack-dev-server"
        },
 * npm run start
