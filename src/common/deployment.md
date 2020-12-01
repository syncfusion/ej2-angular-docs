# Deployment

## CDN

The CDN links are provided individually for all the scripts and style sheets of Syncfusion Angular UI Components (Essential JS 2).

The CDN links are provided to following files in the package

1. UMD Files
2. CSS Files

_The latest minified versions of all UMD, Global and CSS files are available in CDN:_

* **`https://cdn.syncfusion.com/ej2/PACKAGENAME/dist/PACKAGENAME.umd.min.js`**
* **`https://cdn.syncfusion.com/ej2/PACKAGENAME/styles/THEMENAME.css`**

For example

* [https://cdn.syncfusion.com/ej2/ej2-angular-inputs/dist/ej2-angular-inputs.umd.min.js](https://cdn.syncfusion.com/ej2/ej2-angular-inputs/dist/ej2-angular-inputs.umd.min.js)
* [https://cdn.syncfusion.com/ej2/ej2-angular-inputs/styles/material.css](https://cdn.syncfusion.com/ej2/ej2-angular-inputs/styles/material.css)

_Versioned files are also available in CDN._

* **`https://cdn.syncfusion.com/ej2/VERSION/PACKAGENAME/dist/PACKAGENAME.umd.min.js`**
* **`https://cdn.syncfusion.com/ej2/VERSION/PACKAGENAME/styles/THEMENAME.css`**

For example

* [https://cdn.syncfusion.com/ej2/16.4.55/ej2-angular-inputs/dist/ej2-angular-inputs.umd.min.js](https://cdn.syncfusion.com/ej2/16.4.55/ej2-angular-inputs/dist/ej2-angular-inputs.umd.min.js)
* [https://cdn.syncfusion.com/ej2/16.4.55/ej2-angular-inputs/styles/material.css](https://cdn.syncfusion.com/ej2/16.4.55/ej2-angular-inputs/styles/material.css)

## Packages

Syncfusion Angular UI Components (Essential JS 2) packages is published and available in public
[npm](https://www.npmjs.com/search?q=ej2-angular&page=1&ranking=optimal) registry.

### Anatomy of NPM Packages

Syncfusion Angular UI Components (Essential JS 2) are shipped as npm packages. Following
table explains the purpose of each file available in the package.

|    Files                                                                  |    Purpose                                                                                                                                                                                                                                                                                   |
|---------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    `dist/<packagename>.umd.min.js`   `dist/<packagename>.umd.js`              |        For applications using AMD or Common JS based   module loader can be utilize these files.                                                                                                                                                                                             |
|    `src/`                                                                   |    This folder contains the script files in ES6 format. It can be utilize Bundling.                                                                                                                                                         |
|    `styles/<theme_name>.css`      `styles/<theme_name>.scss`                     |    This folder contains the CSS and SCSS files of the package.                                                                                                                                                                                                                             ||