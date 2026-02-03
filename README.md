HARMONI Lab — local preview & production notes

Quick preview (no build):

1. Start a static server in the repo root:

```bash
python3 -m http.server 8000
```

2. Open http://localhost:8000

Why you saw console warnings

- The site currently uses the CDN Tailwind script and the in-browser Babel transformer. These are convenient for demos but not recommended for production:
  - Tailwind CDN doesn't purge unused CSS in production and can be slower. Use the Tailwind CLI or PostCSS plugin to build a minimized stylesheet.
  - babel-standalone transforms in the browser and can break when using certain target/browser combinations; precompile your JSX/ESM code with `@babel/cli` or a bundler.

Suggested minimal production setup

1. Install dev deps:

```bash
npm install --save-dev tailwindcss @babel/cli @babel/core
```

2. Create a `src/input.css` with Tailwind directives:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

3. Build Tailwind once:

```bash
npx tailwindcss -i ./src/input.css -o ./dist/tailwind.css --minify
```

4. Replace the CDN script in each HTML file with a local link to `dist/tailwind.css` and precompile your scripts with Babel.

Optional: use a small bundler (Vite/Parcel) for convenience.

If you'd like, I can scaffold the `src/` folder, create the Tailwind input file, and update the HTML to reference the built CSS — tell me to proceed and I will implement it and run a quick local build.
