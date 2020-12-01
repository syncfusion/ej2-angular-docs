# How to use SCSS file in Angular-cli

## SASS variables location

The SASS variables for Essential JS 2 components are available in the following mentioned location.

`node_modules/@syncfusion/package-name/styles/themename.scss`

For example, refer to the following location for navigation component’s SASS variable.

`node_modules/@syncfusion/ej2-angular-grids/styles/material.scss`

## Initialization of SCSS variables

Refer to the styles of the required component in the src/styles.scss file.

```typescript
@import “ej2-grids/styles/material.scss”
```

## Configuring node SCSS in .angular-cli.json

To avoid SCSS compilation issues and to map the SCSS file path, add the stylePreprocessorOptions to the .angular-cli.json file.

Add the `stylePreprocessorOptions` option under apps in the `.angular-cli.json` file.

The following paths can be used globally in Angular app.

```typescript
"stylePreprocessorOptions": {
         "includePaths": [
         "node_modules/@syncfusion"
        ]
  },
```

An angular sample with SCSS compilation to render the Essential JS 2 Grid component can be downloaded from the following [GitHub link](https://github.com/SyncfusionExamples/ej2-angular-scss).

## How To Override styles

In syncfusion Angular components, you can override control styles by replacing `sass` variable values like below:

```html

// SASS Variable override
$accent: black;
$primary: rgb(0, 255, 157);

// syncfusion styles
@import '../node_modules/@syncfusion/ej2-angular-grids/styles/material.scss';

```

## Angular-cli Version 8 With SASS

In version 8, Angular Team moved away from `node-sass` in favour of `sass`.Nonetheless we have the option to use `node-sass` manually. Use the below command to install `node-sass`:

```bash
npm install node-sass --save-dev
```
