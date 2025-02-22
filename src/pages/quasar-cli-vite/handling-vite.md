---
title: Handling Vite
desc: (@quasar/app-vite) How to manage Vite in a Quasar app.
related:
  - /quasar-cli-vite/quasar-config-js
---

The build system uses [Vite](https://vitejs.dev) to create the UI of your website/app (`/src` folder). Don't worry if you aren't acquainted with Vite. Out of the box, you won't need to configure it because it already has everything set up.

## 用法 with quasar.config.js

For cases where you need to tweak the default Vite config you can do so by editing `/quasar.config.js` and configuring `build > extendViteConf (viteConf)` method.

```js
// quasar.config.js
build: {
  extendViteConf (viteConf, { isServer, isClient }) {
    // do something with viteConf... change it in-place
  }
}
```

Notice that you don't need to return anything. The parameter of extendViteConf(viteConf) is the Vite configuration Object generated by Quasar for you. You can add/remove/replace almost anything in it, assuming you really know what you are doing. Do not tamper with the input and output files though or any other option that is already configured by quasar.config.js > build.

## Inspecting Vite Config
Quasar CLI offers a useful command for this:

```bash
$ quasar inspect -h

  Description
    Inspect Quasar generated Vite config

  Usage
    $ quasar inspect
    $ quasar inspect -c build
    $ quasar inspect -m electron -p 'build.outDir'

  Options
    --cmd, -c        Quasar command [dev|build] (default: dev)
    --mode, -m       App mode [spa|ssr|pwa|bex|cordova|capacitor|electron] (default: spa)
    --depth, -d      Number of levels deep (default: 2)
    --path, -p       Path of config in dot notation
                        Examples:
                          -p module.rules
                          -p plugins
    --thread, -t     Display only one specific app mode config thread
    --help, -h       Displays this message
```

## Adding Vite plugins

Make sure to yarn/npm install the vite plugin package that you want to use, then edit `/quasar.config.js`:

```js
build: {
  vitePlugins: [
    [ '<plugin-name>', { /* plugin options */ } ]
  ]
}
```

There are multiple syntaxes supported:

```js
vitePlugins: [
  [ '<plugin1-name>', { /* plugin1 options */ } ],
  [ '<plugin2-name>', { /* plugin2 options */ } ],
  // ...
]

// or:

vitePlugins: [
  [ require('<plugin1-name>'), { /* plugin1 options */ } ],
  [ require('<plugin2-name>'), { /* plugin2 options */ } ],
  // ...
]

// finally, you can specify using the form below,
// but this one has a drawback in that Quasar CLI cannot pick up
// when you change the options param so you'll have to manually
// restart the dev server

vitePlugins: [
  require('<plugin1-name>')({ /* plugin1 options */ }),
  require('<plugin2-name>')({ /* plugin2 options */ })
  // ...
]
```

::: tip
You might actually bump into Vite plugins that need to be used as `require('<package-name>').default` instead of `require('<package-name>')`. So:

<br>

```js
vitePlugins: [
  [ require('<plugin1-name>').default, { /* plugin1 options */ } ],
  // ...
]
```
:::

And, should you want, you can also add Vite plugins through `extendViteConf()` in `/quasar.config.js`. This is especially useful for (but not limited to) SSR mode where you'd want a Vite plugin to be applied only on the server-side or the client-side:

```js
build: {
  extendViteConf (viteConf, { isClient, isServer }) {
    viteConf.plugins.push(
      require('<plugin1-name>')({ /* plugin1 options */ }),
      require('<plugin2-name>')({ /* plugin2 options */ })
      // ...
    )
  }
}
```

Moreover, don't forget that your `/quasar.config.js` exports a function that receives `ctx` as parameter. You can use it throughout the whole config file to apply settings only to certain Quasar modes or only to dev or prod:

```js
module.exports = function (ctx) {
  return {
    build: {
      extendViteConf (viteConf, { isClient, isServer }) {
        if (ctx.mode.pwa) {
          viteConf.plugins.push(/* ... */)
        }

        if (ctx.dev) {
          viteConf.plugins.push(/* ... */)
        }
      }
    }
  }
}
```

## Folder aliases
Quasar comes with a bunch of useful folder aliases preconfigured. You can use them anywhere in your project and Vite will resolve the correct path.

| Alias | Resolves to |
| --- | --- |
| `src` | /src |
| `app` | / |
| `components` | /src/components |
| `layouts` | /src/layouts |
| `pages` | /src/pages |
| `assets` | /src/assets |
| `boot` | /src/boot |
| `stores` | /src/stores (Pinia stores) |

#### Adding folder aliases

To add your own alias there are two ways:

1. Edit `/quasar.config.js`:

```js
// quasar.config.js
const path = require('path')

module.exports = function (ctx) {
  return {
    build: {
      alias: {
        myalias: path.join(__dirname, './src/somefolder')
      }
    }
  }
}
```

2. Alternatively, you can directly extend the Vite config and merge it with the existing alias list. Use the `path.join` helper to resolve the path to your intended alias.

```js
// quasar.config.js
const path = require('path')

module.exports = function (ctx) {
  return {
    build: {
      extendViteConf (viteConf, { isServer, isClient }) {
        Object.assign(viteConf.resolve.alias, {
          myalias: path.join(__dirname, './src/somefolder')
        })
      }
    }
  }
}
```

## PostCSS

Styles in `*.vue` files (and all other style files) are piped through PostCSS by default, so you don't need to use a specific loader for it.

By default, PostCSS is configured to use Autoprefixer. Take a look at `/postcss.config.js` where you can tweak it if you need to.
