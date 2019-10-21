# sapper-template-hot

A clone of the default [Sapper](https://github.com/sveltejs/sapper) template, with added support for HMR. Available for Rollup and webpack.


## Status

Svelte HMR support is still quite experimental. Not ready for production. (But you won't ship your HMR, right?)


## From scratch


### Using `degit`

[`degit`](https://github.com/Rich-Harris/degit) is a scaffolding tool that lets you create a directory from a branch in a repository. Use either the `rollup` or `webpack` branch in `sapper-template`:

```bash
# for Rollup
npx degit "rixo/sapper-template-hot#rollup" my-app
# for webpack
npx degit "rixo/sapper-template-hot#webpack" my-app
```


### Running the project

However you get the code, you can install dependencies and run the project in development mode with:

```bash
cd my-app
npm install # or yarn
npm run dev
```

Open up [localhost:3000](http://localhost:3000) and start clicking around.

Consult [sapper.svelte.dev](https://sapper.svelte.dev) for help getting started.

This project intends to stick to the [official template](https://github.com/sveltejs/sapper-template) as much as possible, so refer to its docs for all details about the template itself.


## Add it to your project

~~~bash
# replace svelte-loader with fork with HMR support
npm install -D rixo/svelte-loader
~~~

Adapt your `webpack.config.js` (considering you started from the official template):

~~~js
const hot = dev && process.env.HOT != 0

module.exports = {
  client: {
    ...
    module: {
      rules: [
        {
          test: /\.(svelte|html)$/,
          use: {
            loader: 'svelte-loader',
            options: {
              dev, // NOTE dev mode is REQUIRED for HMR
              hydratable: true,
              hotReload: hot,
              hotOptions: {
                // optimistic will try to recover from runtime errors during
                // component init (instead of doing a full reload)
                optimistic: true,
              },
            },
          },
        },
      ],
    },
    ...
    plugins: [
      // pending https://github.com/sveltejs/svelte/issues/3632
      hot && new webpack.HotModuleReplacementPlugin(),
      ...
    ].filter(Boolean),
  },
  ...
}
~~~


## Bugs and feedback

HMR is not officially supported by Svelte (yet?), so please report issues & feedback about HMR in [this project's issue tracker](https://github.com/rixo/sapper-template-hot/issues).
