# Installation 

```
mkdir <foldername>
npm init -y 
npm install tailwindcss autoprefixer postcss-cli
npx tailwindcss init
touch postcss.config.js
nano postcss.config.js
```

## Add the next code: 

```
module.exports = {
    plugins: [
        require('tailwindcss'),
        require('autoprefixer')
    ]
}
```

## Create a tailwind.css file

```
mkdir src/css/tailwind.css
nano src/css/tailwind.css
```

## Add the next code to tailwind.css file

```
@tailwind base;

@tailwind components;

@tailwind utilities;
```

## Build tailwind css file 

```
nano package.json
//on scripts key add
"build": "postcss src/css/tailwind.css -o public/css/style.css"
```

## Create Public folder with an HTML file

```
mkdir public
cd public
touch index.html
```

## Generate css file for tailwind

```
npm run build
```

## then just add your style tag on index.html file

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="css/style.css">
    <title>Hello world!</title>
</head>
<body>
    <h1>Hello world!</h1>
</body>
</html>
```

## To add a full config file

```
npx tailwindcss init tailwind.config.full.js --full
```

# Deploy 

## Discard all css useless for the project 

```
npm i -D @fullhuman/postcss-purgecss
```

Then in postcss.config.js file add a const with the library and add it in plugins key

```
const purgecss = require('@fullhuman/postcss-purgecss')

module.exports = {
  plugins: [
    purgecss({
      content: ['./**/*.html'],
      defaultExtractor: content => content.match(/[\w-/:]+(?<!:)/g) || [],
    })
  ]
}
```

* Remember defaultExtractor is used to maintain all css rules of the breakpoints

Execute the build, watch or dev command, and go to your styles.css file then you would be able to see only used css rules.

## Minify css

```
npm install cssnano --save-dev
```

In your postcss.config.js file add the nanocss plugin

```
const purgecss = require("@fullhuman/postcss-purgecss");

module.exports = {
  plugins: [
    require("tailwindcss"),
    require("autoprefixer"),
    purgecss({
      content: ["./**/*.html"],
      defaultExtractor: content => content.match(/[\w-/:]+(?<!:)/g) || [],
    }),
    require("cssnano")({
      preset: "default",
    }),
  ],
};
```

Then re-run (build, watch or dev command) and now your "public" folder is ready for production