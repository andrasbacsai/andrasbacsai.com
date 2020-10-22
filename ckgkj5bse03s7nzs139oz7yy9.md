## Straightforward guide to use TailwindCSS with Sapper

There are many articles online on integrating Tailwind into Next.js/Nuxt.js, but there are only a few ones for [Sapper](https://sapper.svelte.dev/). 

Most of them are:
- outdated,
- very complicated,
- doesn't allow to use of all features of TailwindCSS, like `@apply`.

Some of them are making the development flow a real nightmare—for example, 30 secs of hot module reloading time. 😵 

I spent hours figuring out the best way to integrate it into Sapper, so you don't need to. 

> This tutorial assumes you are familiar with the terms and commands I will use. I'm not going into deep details about them to keep this article short and simple (and concise).

# Initial Sapper setup

Create an initial clone of the official sapper template - rollup version.

```
npx degit "sveltejs/sapper-template#rollup" sapper-tailwind && cd sapper-tailwind
``` 

It will create a directory named `sapper-tailwind` with a basic Sapper configuration.

# Typescript (optional)

If you would like to use Typescript, execute the following command before you do anything. Otherwise, your changes could be lost.

```bash
node scripts/setupTypeScript.js
```

This is totally optional if you are not sure that you need Typescript or not, you probably not! (Don't follow the hype!)

# Add the required packages

```none
yarn add -D cssnano npm-run-all postcss postcss-cli \
postcss-import postcss-load-config postcss-preset-env \
svelte-preprocess tailwindcss
```

`cssnano` to make the production CSS as small as possible.

`npm-run-all` to run package.json scripts in parallel or sequential - you will see why.

`postcss*` packages, obviously for [PostCSS](https://postcss.org/).

`svelte-preprocess` to preprocess other languages like Typescript or SCSS. It also helps [svelte-vscode](https://marketplace.visualstudio.com/items?itemName=svelte.svelte-vscode) extension to understand your code before preprocessing in VSCode.

`tailwindcss` - no idea why it's needed 😁.

# Configure tailwind

This will create a `tailwind.config.js` in your root directory:

```
npx tailwind init
```

We need to tweak the default configuration to look like this:

```js
module.exports = {
  future: {},
  purge: {
    mode: 'all',
    content: ['./src/**/*.svelte', './src/**/*.html'],
  },
  theme: {
    extend: {},
  },
  variants: {},
  plugins: [],
}
```

Allowing purge helps us to remove all the unnecessary CSS classes from the production bundle. That is what you definitely needed because Tailwind with all the classes and stuffs is heavy (~1.4MB).

# Create Svelte configuration

Drop the following content to `svelte.config.js` in the root directory:

```js
import autoProcess from 'svelte-preprocess';
export const preprocess = autoProcess({ postcss: true });
```

This will allow you to use many syntax sugar languages in Svelte and tell VSCode how to process that much sugar.

# Modify Rollup configuration

We need to add the preprocess method to our rollup configuration. Otherwise, rollup won't know what to do.

Rollup.config.js` has a default export, which consists of 3 sections:
- Client
- Server
- Service worker

Each has its own plugin configuration. We need to add preprocess to our `client` & `server` section, exactly to the `svelte` plugin part:

```js
import { preprocess } from './svelte.config';
// client
svelte({
   dev,
   hydratable: true,
   emitCss: true,
   _preprocess_
})
// server
svelte({
   generate: 'ssr',
   hydratable: true,
   dev,
   _preprocess_
}),
```

# Create PostCSS config

Add a `postcss.config.js` file to the root directory:

```js
const tailwind = require('tailwindcss');
const cssnano = require('cssnano');
const postcssImport = require('postcss-import');
const presetEnv = require('postcss-preset-env')({
  features: {
    'nesting-rules': true, // Optional, not necessary. Read details about it  [here](https://tabatkins.github.io/specs/css-nesting/#motivation) 
  },
});

const plugins =
  process.env.NODE_ENV === 'production'
    ? [postcssImport, tailwind, presetEnv, cssnano]
    : [postcssImport, tailwind, presetEnv];

module.exports = { plugins };
```

# Modify package.json

Add the following scripts to `package.json` file:

```
  "scripts": {
    "watch:css": "postcss src/assets/global.pcss -o static/global.css -w",
    "watch:dev": "sapper dev",
    "dev": "run-p watch:*",
    "build": "run-s build:css build:sapper",
    "build:css": "NODE_ENV=production postcss src/assets/global.pcss -o static/global.css",
    "build:sapper": "sapper build",
    "build:export": "sapper export",
    "export": "run-s build:css build:export",
    "start": "node __sapper__/build",
    "serve": "serve ___sapper__/export"
  },
```

Don't worry. You do not need to use all of them. 

1. To develop, use`yarn dev` to preprocess TailwindCSS in watch mode (`watch:css` script) and start sapper development (`watch:dev`).
2. To build, `yarn build`, which also preprocess tailwind, but in `production` mode, it eliminates unused classes + minify the final CSS files. Also builds application related files.
3. To start production SSR, `yarn start` - simple.

> Note: I removed the `--legacy` flags from the build commands because I have no good argument to support old browsers.

# Import Tailwind into your application

Create the following directory `src/assets/` and place a PostCSS file (`global.pcss` for example) which imports Tailwind configurations:

```
// src/assets/global.pcss
@tailwind base;
@tailwind components;
@tailwind utilities;
```

We are done! 🎉

# Conclusion

It was a wacky ride. You persisted to the end. I'm proud of you. 👏

You deserve the full code in a [repository](https://github.com/andrasbacsai/sapper-tailwind-starter).

 ---

> If you liked this article, let me know by following me on  [Twitter](https://twitter.com/andrasbacsai). Feel free to contact me there or let me if you know a better way to do it!

---


> <span>Cover photo by <a href="https://unsplash.com/@aronvisuals?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Aron Visuals</a> on <a href="https://unsplash.com/s/photos/guide?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Unsplash</a></span>