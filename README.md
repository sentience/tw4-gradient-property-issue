# Tailwind v4.1.5 bug report

This page demonstrates an issue ([tailwindlabs/tailwindcss#17845](https://github.com/tailwindlabs/tailwindcss/issues/17845)) that occurs when a component library with Tailwind 3 generated styles is used in an app with Tailwind 4 styles.

In theory, the Tailwind 3 styles have their own prefix (`tw3-`) and are loaded into the `components` CSS cascade layer, so they should not interfere with the Tailwind styles in the consuming app.

In practice, Tailwind 4 registers `--tw-gradient-from` as a `@property` that must contain a `&lt;color&gt;` value, but in the Tailwind 3 generated styles, `--tw-gradient-from` contains a color followed by a percentage (`#6b7280 var(--tw-gradient-from-position)`). This value is discarded by the browser as invalid, which breaks the TW3-generated gradient.

A fix for this could be to change the name of the variable in TW4 to something that doesn't clash with TW3, like `--tw-gradient-from-color`.

## Preview

This is what the reproduction looks like in a browser:

![screenshot of the demo](./demo.png)

## How to run

For convenience, all of the build output is included in this repo. To see the reproduction, just clone this repo and open the **index.html** file in a browser.

If you want to re-run the Tailwind 4 build of the app's styles, you can do this from the root directory:

```sh
pnpm i
pnpm build
```

If you want to re-run the Tailwind 3 build of the package's styles, you can do this from the **tw3-package** directory:

```sh
cd tw3-package
pnpm i
pnpm build
```
