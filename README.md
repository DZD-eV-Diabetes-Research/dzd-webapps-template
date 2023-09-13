# DZD Vue Frontend Template

This project is setup to be used as an template for [VueJS](https://vuejs.org/) WebApp frontend. 

The template uses [Vite](https://vitejs.dev/) as an build tool. It also comes with a Gitlab & Docker configuration, which builds the App and serves the build as static files.

The template is derived from [dzd-micemen](https://github.com/DZD-eV-Diabetes-Research/dzd-micemen), which can also be used for a reference on how different components can be used.

For any questions reach out to philipp@digitalwerft.com.

## Features

UI Examples

- Header, Footer and How-To UI
- Query and Result UI
- Modal UI Example
- Loading Indicator
- Example HTTP Request (PubMed results for given Gene in Humans)
- UI State management (hide result, show loading indicator)

Other

- Example HTTP request
- Gitlab and Docker config

## Files and folders

```
app/                  All frontend code is in this folder for easy dockerization
  dist/               Built target folder, created automatically
  src/                All JS and Vue files live in this folder
    components/       All Vue components life in this folder
      Layout/         Reuseable design components
        Footer.vue    Logos and Link to Imprint
        Header.vue    App title and description
        Layout.vue    Parent layout component, also contains About and How-To text
    lib/              Shared code
      api.js          Functions for all HTTP requests to backend
      config.js       Shared app configuration, e.g. Server URLs
      helper.js       Helper function, e.g. Math functions
    styles/           Shared stylesheets as SASS
    App.vue           Parent Vue compontent, loads all other components
    main.js           Main JS file, imports all other JS files
  public/             Static files, e.g. fonts, images, logos
  index.html          Loads and mounts App.vue
  package.json        Project dependencies
  vite.config.js      Vite (Vue build tool) config

```


## Recommended IDE Setup

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur).


## Project Setup

Install dependencies from npm. You can also use `npm` instead of `yarn`.

```sh
cd app/
yarn install
```

### Compile and Hot-Reload for Development

Creates and serves a built of the app with autoreload. See console output for URL.

```sh
cd app/
yarn run dev
```

### Compile and Minify for Production

Creates a build into `app/dist`. Output can be served as static files, e.g. via nginx.

```sh
cd app/
yarn run build
```
## Run Project

### Via prebuild docker image

```bash
docker run -p 80:80 registry-gl.connect.dzd-ev.de:443/dzdapps/dzd-werk:latest
```

### Via local build image

```bash
git clone ssh://git@git.connect.dzd-ev.de:22022/dzdapps/dzd-werk.git
```

```bash
docker build . -t myImageName
```

```bash
docker run -p 80:80 myImageName
```