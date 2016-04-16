---
layout: post
title: Scaffolding a React Web Application
date: 2016-04-12
---
This is the project setup and scaffolding I followed when creating a [React + d3 histogram](http://jamesanaipakos.com/react-d3-data-viz/). By following the below steps for each project, developers can organize their project not only literally with build and production pipelines, and also figuratively by creating a mental model of its working parts. The following sections discuss entities and processes your web application should contain.

## Configuration
The included configuration files are `package.json`, `.babelrc`, `.eslint`, `.esconfig`.


`package.json` is configured normally, with babel config options included as an attribute. `config.json` sets the path for the development and production folders, and is used in the `webpack.js` and `server.js` files for readability and consistency. `.babelrc` enables some ES7 options, specifically the double colons `::`. This is also enabled in `package.json`. `.eslint` and `.econfig` are described more in the Error Handling section.

## Directory Structure

The directory has four folders.
- The production application loads `dist/index.html`, which reads the compiled `bundle.js`. Any change that needs to be reflected in production, the user should use the `npm run postinstall` script to run the production Webpack file and compile a new `dist/bundle.js`.
- `css/` contains the styling. The LESS file is referenced by the main Histogram Component, and bundled together for development. But in production, this styling is loaded as an external CSS file to avoid the Flash Of Unstyled Content.
- `public/data/` contains the data that will be loaded into the gragh. The only place this data is referenced is `/components/index.jsx` and the name of this file and the data include can be changed here.
- `.src/` is where the application Components live. Each Component has its own folder and is imported to other Components accordingly.
- The development application loads `index.html` in the root directory. And the production application loads `index.html` in `/dist`.

## Design Tools
React, ReactDOM, and d3 are used for the design. All three packages are required for production. Scaffolding is in place that allows the user to change the visual layout of the graph easily by going into `src/components/MLGraph/index.jsx` and either changing the graph dimensions or layout. LESS is used for the styling, and its loader is required for production. `webpack.config.js` also includes a pipeline for changing LESS to CSS. The user can plug in any styilng they want. Just place the SCSS or Sass files into `/css` and change the require path in `src/components/MLGraph/index.jsx` and the pipeline in `webpack.config.js`.

Specific to this project, if new data is loaded, then the output text of the Meta Components, e.g. Title and Description, should be changed to reflect the new data subject matter.

## Development Tools
This application is deployed through the `gh-pages` package. It can be installed via `npm i gh-pages --save`. When running it via a script in `package.json`, (in this example the script is written as `'deploy': 'npm gh-pages [src]'`) `gh-pages` pushes the specified folder to the gh-pages branch in your repository. The user can then access the project via `https://[github_name].github.io/[project_repo_name]`. Heroku is also an option here, and the port requirements are already set up in `server.js`. I like the simplicity of `gh-pages` and the ability to track page visits.

## Build Tools
Webpack is used to build the application. Webpack has four main objects: entry output, plugin, modue/loaders.
- Entry is the file that will load the application.
- Output is the location that `bundle.js` will be sent after it hs been built.
- Plugin is any number of Webpack plugins that will help minimize, transform, or hot-reload your application.
- Loaders transpile and processes styles and extensions such as LESS and .jsx.

It is possible to have one Webpack file, and to create two separate streams for development and production. I've opted to have two files. For development, the `webpack-dev-server` package is in place. This is a good start, but future refactorings should use plugins to decrease the file size due to the CSV data file that is loaded.

Webpack is built by the `postinstall` script specified in `package.json`, which runs Webpack, loads the entry location files, and builds the `bundle.js` to the output location.

## Test Tools
The only testing here is `.eslint`. Future refactors will include unit testing.

## Error Handling
A linter is included for the user to run manually. Its functionality can be changed in `.eslintsettings`. As shown in `package.json`, it can be ran with `npm lint [folder]`.

## Databases
There is no database in this release, only a loaded CSV file. Heroku can be used with a PostgreSQL database to improve the speed of loading the data.

This is how I will be setting up future React + D3.js projects.
