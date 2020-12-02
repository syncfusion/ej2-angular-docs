---
title: "Getting Started"
component: "Card"
description: "This section explains how to create a Essential JS 2 Card control in the Angular application with its basic features."
---

# Getting Started

This section explains how to create a simple **Card** using Styles, and
how to configure the structure for the header section, Horizontal, action buttons, content section, and configure its available
 functionalities in Angular using Angular quickstart.

## Dependencies

The Card Component is pure CSS component so no specific dependencies to render the card.

```js
|-- @syncfusion/ej2-layouts
```

## Setup Angular Environment

You can use [`Angular CLI`](https://github.com/angular/angular-cli) to setup your Angular applications.
To install Angular CLI use the following command.

```bash
npm install -g @angular/cli
```

## Create an Angular Application

Start a new Angular application using below Angular CLI command.

```bash
ng new my-app
cd my-app
```

## Adding Syncfusion Layout package

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) registry.

To install Card component, use the following command.

```bash
npm install @syncfusion/ej2-layouts --save
```

> The **--save** will instruct NPM to include the Card package inside of the **dependencies** section of the **package.json**.
> Since Card Component is a pure CSS component
so no need to configure anything except angular package.

## Adding CSS reference

The following CSS files are available in `../node_modules/@syncfusion` package folder.
This can be referenced in [src/styles.css] using following code.

```css
@import '../node_modules/@syncfusion/ej2-base/styles/material.css';  
@import '../node_modules/@syncfusion/ej2-layouts/styles/material.css';  

```

## Adding a simple Card

* Add the HTML `div` element with `e-card` class into your `index.html`.

`[src/index.html]`

```html
        <div class = "e-card">
          Sample Card
        </div>
```

## Adding a header to the card

You can create cards with a header in a specific structure. For adding header you need to create `div` element and add `e-card-header` class.

* You can include heading inside the card header by adding an `div` element with
`e-card-header-caption` class, and also content will be added by adding element with
`e-card-content`. For detailed information, refer to the [Header and Content](./header-content/).

```html
    <div class = "e-card">                    --> Root Element
        <div class="e-card-header">           --> Root Header Element
            <div class="e-card-header-caption">    --> Root Heading Element
                <div class="e-card-header-title"></div>   --> Heading Title Element
            </div>
            <div class="e-card-content"></div>         --> Card content Element
        </div>
    </div>
```

* Now, run the application in the browser using the following command.

```shell
npm start
```

Output will be as follows:

{% tab template="card/card_header", isDefaultActive=true, sourceFiles="app/**/*.ts,index.css" %}

```typescript
import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
        <div tabindex="0" class="e-card" id="basic">
            <div class="e-card-header">
                <div class="e-card-header-caption">
                    <div class="e-card-title">Advanced UWP</div>
                </div>
            </div>
            <div class="e-card-content">
                Communicating with Windows 10 and Other Apps, the second in a five-part series written by Succinctly series
                author Matteo Pagani. To download the complete white paper, and other papers in the series, visit
                the White Paper section of Syncfusion’s Technology Resource Portal.
            </div>
        </div>
        `
})

export class AppComponent {
    @ViewChild('element') element;

}
```

{% endtab %}

## See Also

* [How to add a header and content](./header-content/)