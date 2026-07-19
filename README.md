# Sedric Edwards — High-Velocity Studio

Single-page agency site. SvelteKit + TypeScript + Tailwind CSS, static build.

Live: https://sedricedwards.github.io/agency-site/

## Develop

```sh
npm install
npm run dev -- --open
```

## Deploy

```sh
$env:BASE_PATH='/agency-site'; npm run build
npx gh-pages -d build -t
```

`BASE_PATH` is only needed for GitHub Pages; omit it when hosting at a domain root.
