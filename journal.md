---
title: Project Journal
author: Matthias Lampert
date: 2023-01-26
---

# TODO

# JOURNAL

## 2023-01-27 07:40

All right. Since Bulma no longer works the easy way (and I don't really need it), 
I had to do a few jobs Bulma was doing for me, using the following packages:

```json
"dependencies": {
  "@fontsource/poppins": "^4.5.10",
  "sanitize.css": "^13.0.0"
}
```


## 2023-01-26 16:56

New Game, new luck. Had some tough moments with this one. _Svelte-add_ no longer
works with the newest version of Vite and SvelteKit. However, I can still use
Sass for this project, which helps. Here's how I installed it

```bash
$ pnpm install -D sass
$ pnpm install -D svelte-preprocess 
```

And then I added this in `svelte.config.js`:

```javascript
import preprocess from 'svelte-preprocess'
```

Finally, I added this into the `<style lang="scss">` part of the `+page.svelte` component:

```css
@import './src/app.scss';
h1 {
  color: $link-color;
}
```

The `@import` part includes global settings in the imported file.
