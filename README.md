# Javascript Toolkit WebSite [![Build Status](https://snap-ci.com/u0q-pWK3MpXCrxJpr84gJQizhRQHHSHA762_g6sBQzM/build_image)](https://snap-ci.com/trecenti/javascript-toolkit/branch/master)

Source code repository for [javascript-toolkit.com](http://javascript-toolkit.com)


## Development

### Architecture

We use metalsmith to generate a static website aplying the `.ejs` templates `/templates/*` from `json` content defined in `/src/**/*.json`. Any other static `/src/**/*.html` or `/src/image/*` file will also be copied to the `/build` directory.

Stylesheets are being pre-processed by `sass` and must live inside the `/src/sass/` folder, this will output `.css` files that are going to be used for each of the template pages that we have. (home, category, tool)

Here's the current architecture to generate the static website, given the structure:
```
/src
  |__/category
  |  |__/sub-category
  |     |__index.json
  |     |__tool.json
  |__index.json
```

it will output:
```
/build
  |__/sub-category
  |  |__index.html
  |__index.html
```

The template will be selected based on where the `.json` is located and its name, for example:

`/src/index.json` uses `/templates/home.ejs`

`/src/category/sub-category/index.json` uses `/templates/category.ejs`

`/src/category/sub-category/tool.json` will be baked into `/templates/category.ejs`

### Scripts

Watch for changes on `/src` and `/templates` and build the static website. Useful for fast interaction development.
```bash
npm run watch
```

Serve the static website structure from `/build` on `localhost:$PORT` where `$PORT` is a env variable declared which is default to 4000
```bash
npm start
```

Manually build the stucture outputing to `/build`
```bash
npm run build
```

### Testing

We're using nightwatch to create end-2-end functional UI tests, we should write tests whenever a new tool is added to the toolkit.


## Environment & Deploys

### Production
We're using Github Pages to host the website, deploys to production are manually triggered from [Snap-ci](https://snap-ci.com/ThoughtWorksInc/js-toolkit/branch/master), we plan to automate this once we have a release.

### Staging
We have a staging environment hosted [heroku](http://staging-js-toolkit.herokuapp.com), every merge to master will deploy a new version of the app to this env.
Tests will also be run in this environment, they're managed by Snap-Ci

### Publishing Changes

Publish `/build` to `gh-pages` branch.

**Use with caution**: this is the production deploy mechanism, we shouldn't run this command via terminal. Instead refer to [production section](#Production) of this readme for deploys to production.
```bash
npm run publish
```
There's a helper that builds and publish.
```bash
npm run buildAndPublish
```

