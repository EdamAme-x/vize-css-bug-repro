# Vize CSS Reproduction

This repository demonstrates that `@vizejs/vite-plugin` can emit extracted Vue SFC scoped CSS without linking it from the generated production HTML.

## Reproduce

```sh
pnpm install
pnpm build
grep -n "stylesheet" dist/index.html
find dist/assets -maxdepth 1 -type f -name "*.css" -print
```

## Expected

The production HTML should load all CSS required by the Vue SFC. The page should have a black background from `src/App.vue`'s scoped style.

## Actual

`dist/assets/vize-components.css` is emitted, but `dist/index.html` does not reference it. The browser therefore does not load the Vue SFC scoped CSS.

Observed with this repository:

```html
<script type="module" crossorigin src="/assets/index-9RXv6tjC.js"></script>
```

There is no stylesheet link in `dist/index.html`, while `dist/assets/vize-components.css` exists.

## Workaround

Importing Vize's virtual styles module from the entry file makes the required CSS part of the linked Vite CSS asset:

```js
import 'virtual:vize-styles'
```

## Environment

- `@vizejs/vite-plugin`: `0.124.0`
- `vite`: `8.0.14`
- `vue`: `3.5.33`
- Node.js: `>=22`

This also occurred in a real project:

- Broken commit: https://github.com/EdamAme-x/rinri/tree/2924b8a4d4dc30300c5db613fd21df42d6fc8429
- Workaround commit: https://github.com/EdamAme-x/rinri/commit/84b8272
