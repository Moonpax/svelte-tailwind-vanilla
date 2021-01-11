# Svelte 3 with Tailwind 2 vanilla

![](https://upload.wikimedia.org/wikipedia/commons/thumb/1/1b/Svelte_Logo.svg/199px-Svelte_Logo.svg.png) ![](https://seeklogo.com/images/T/tailwind-css-logo-5AD4175897-seeklogo.com.png)

Setting up Tailwind with Svelte is really simple, just install necessary dependencies:

```sh
npm i -D svelte-preprocess tailwindcss postcss autoprefixer
```

Configure **svelte-preprocess** in `rollup.config.js`

```js
import svelte from 'rollup-plugin-svelte';
import resolve from '@rollup/plugin-node-resolve';
import commonjs from '@rollup/plugin-commonjs';
import livereload from 'rollup-plugin-livereload';
import { terser } from 'rollup-plugin-terser';
import sveltePreprocess from 'svelte-preprocess'; // add here

// ...

export default {
  // ...
  plugins: [
    svelte({
      // ...
      // add here
      preprocess: sveltePreprocess({
        postcss: {
          plugins: [require('tailwindcss'), require('autoprefixer')],
        },
      }),
    }),
    // ...
  ],
  // ...
};
```

Create Tailwind.svelte component in `src/` folder:

```svelte
<style global>
  @import 'tailwindcss/base';
  @import 'tailwindcss/components';
  @import 'tailwindcss/utilities';
</style>
```
Next, just import Tailwind.svelte in `src/App.svelte`

```svelte
<script>
	import Tailwind from "./Tailwind.svelte";
</script>
```

Create Tailwind config file

```sh
npx tailwindcss init
```

Finally, configure `purge` in `tailwind.config.js`:

```js
module.exports = {

  purge: {
    enabled: true,
    content: ['./src/**/*.svelte'],
  },
  darkMode: false, // or 'media' or 'class'
  theme: {
    extend: {},
  },
  variants: {
    extend: {},
  },
  plugins: [],
};
```
# Svelte

This is a project template for [Svelte](https://svelte.dev) apps. It lives at https://github.com/sveltejs/template.

To create a new project based on this template using [degit](https://github.com/Rich-Harris/degit):

```bash
npx degit sveltejs/template svelte-app
cd svelte-app
```

*Note that you will need to have [Node.js](https://nodejs.org) installed.*


## Get started

Install the dependencies...

```bash
cd svelte-app
npm install
```

...then start [Rollup](https://rollupjs.org):

```bash
npm run dev
```

Navigate to [localhost:5000](http://localhost:5000). You should see your app running. Edit a component file in `src`, save it, and reload the page to see your changes.

By default, the server will only respond to requests from localhost. To allow connections from other computers, edit the `sirv` commands in package.json to include the option `--host 0.0.0.0`.

If you're using [Visual Studio Code](https://code.visualstudio.com/) we recommend installing the official extension [Svelte for VS Code](https://marketplace.visualstudio.com/items?itemName=svelte.svelte-vscode). If you are using other editors you may need to install a plugin in order to get syntax highlighting and intellisense.

## Building and running in production mode

To create an optimised version of the app:

```bash
npm run build
```

You can run the newly built app with `npm run start`. This uses [sirv](https://github.com/lukeed/sirv), which is included in your package.json's `dependencies` so that the app will work when you deploy to platforms like [Heroku](https://heroku.com).


## Single-page app mode

By default, sirv will only respond to requests that match files in `public`. This is to maximise compatibility with static fileservers, allowing you to deploy your app anywhere.

If you're building a single-page app (SPA) with multiple routes, sirv needs to be able to respond to requests for *any* path. You can make it so by editing the `"start"` command in package.json:

```js
"start": "sirv public --single"
```

## Using TypeScript

This template comes with a script to set up a TypeScript development environment, you can run it immediately after cloning the template with:

```bash
node scripts/setupTypeScript.js
```

Or remove the script via:

```bash
rm scripts/setupTypeScript.js
```

## Deploying to the web

### With [Vercel](https://vercel.com)

Install `vercel` if you haven't already:

```bash
npm install -g vercel
```

Then, from within your project folder:

```bash
cd public
vercel deploy --name my-project
```

### With [surge](https://surge.sh/)

Install `surge` if you haven't already:

```bash
npm install -g surge
```

Then, from within your project folder:

```bash
npm run build
surge public my-project.surge.sh
```
