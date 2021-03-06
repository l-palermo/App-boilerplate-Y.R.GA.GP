# App-boilerplate-P.R.GA.GP

`todos:`
> review Linaria settings

> find out more about rollup plugin order


> find out more about bable bundle worning


Deployed at: https://l-palermo.github.io/App-boilerplate-P.R.GA.GP/

Most of the reasoning behind this boilerplate derives from this <a href="https://github.com/l-palermo/App-boilerplate-Y.W.L.DO.C">previous work</a> part of the same series of exercise.

PNPM

Pnpm is an alternative tool to yarn and npm that declare to be faster than both its competitors. This benchmark is an example of installation and update of packages in a react app. <a href='https://github.com/pnpm/benchmarks-of-javascript-package-managers'>Benchmark</a>.

Pnpm keeps the packages in a global store on the local machine, then it creates a hard link from it instead of copying the packages so for each version of a module, there is only ever one copy kept on disk.
Npm and Yarn both have a deep dependency tree with packages copied several times and the algorithm to flatten the d tree is complex and burn resources. Pnpm has a flat dependency structure and uses symlinks to group them together, this allows for better use of resources and higher computational speed.
The duplicated packages often force the use of larger CI/CD resources and time.
The package JSON structure created with `pnpm init` is slightly different from the one created with NPM or YARN.

Install:

`curl -L https://raw.githubusercontent.com/pnpm/self-installer/master/install.js | node`

---

Rollup is a very popular javascript module bundler. It uses ES2015 format to rewrite the code and try to create smaller builds with the help of dead code elimination or tree-shaking.

It has many plugins and functionalities out of the box that webpack doesn't have like node polyfills for import/export and supports relative paths in the config.
The numerous plugins might bring some confusion this is also because there are no so many discussions on these plugins on the web so
the developer needs to choose carefully. For example, in the docs, the 'rollup-plugin-style' is advised above the other, it does lots of cool things and supports different formats as SASS, POST-CSS, LESS etc, but it bundles the CSS inside the js bundle file and the docs are not clear on what is happening
under the hood but the CSS seems to be embedded into the js file and this might then require further computation. It's no clear how rollup or the plugin will handle this.

The reesources on the web are confusing and not updated, it easy to find pages like this https://github.com/rollup/awesome with a bunch of useful plugin that unfortunately are deprecated and other pages like this https://github.com/rollup/plugins where there is a list of the new one. However the docs are not great and for a beginner is all a bit confusing. On the contrary I find webpack doc much more clearer and easy to navigate.

Positive note, the bundle speed is good so far and the live reload function also works great.

Install:

`pnpm add -D rollup rollup-plugin-serve rollup-plugin-livereload rollup-plugin-generate-html-template rollup-plugin-clear rollup-plugin-css-porter @rollup/plugin-url @rollup/plugin-image`

---

BABEL, REACT

Configuring Rollup for babel and react requires a bunch of plugins:

Install:

`pnpm add react react-dom`

`pnpm add -D @rollup/plugin-node-resolve @rollup/plugin-commonjs @rollup/plugin-babel @babel/preset-react @babel/preset-env @babel/core rollup-plugin-node-globals`

---

JEST, REACT TESTING LIBRARY

Jest is still the testing framework of choice for various reasons like great support and discussion on the web about different topics and issues, it is fairly quick, fairly easy to set up and does what it is required to do well. Moreover, most of the React Testing Library code examples are base on the Jest testing framework.
A fairly similar alternative would be Mocha.

React testing library is a great tool and I want to re-adopt it also in this boilerplate to get more confidence with it.

---

ESLINT, PRETTIER, HUSKY, A11Y

These three tools are still my favorite choice. They do what they need to do, the docs are good and there is a lot of support on the web for different use cases.
This helps me in maintaining code redability, facilitating my dev experience and focuses on more important things.

A11Y is linter tool for accessibility. It is suggested by React and it will definitely help me in writing more accessible code.

---

GITHUB PAGES, GITHUB ACTIONS

This time decided to go full-on with GitHub. GitHub actions are very easy to setup and help with keeping good quality workflow, reducing bugs and making sure the code passes the tests and build correctly before being merged to master. More actions can be set up to improve the deployment process.
About Github Pages instead, the way it works is still a bit cryptic for me and require some more investigations. There is a good amount of docs on how to deploy docs but not much information on how to lead GitHub pages to look for the built file in the folder of our choice. Apparently it wants the built to be in the root folder and that's why the gh-pages plugin automatically creates a gh-pages branch where stores the built. I guess this is what every other hosting provider does under the hood but doesn't seem nice having a stale branch on our repo.

---

LINARIA

I like writing `CSS in JS` and Linaria is becoming a popular tool to avoid adding runtime to your app. I have already initialized the previous Boilerplate with Linaria and now I want to test how easy/possible is adding it using the Rollup bundler.

Installing Linaria is not as straight forward as it is with Webpack. Babel needs to be configured via a .babelrc file because configuring Babel via the Babel-Rollup-plugin generates compiling errors from Linaria. I haven't found much information on why this happen but it seems due to the order in wich the code get transpiled by each plugin. Also a bunch of other missing dependencies error came out but were easily resolvable.

Overall it works as expected.
