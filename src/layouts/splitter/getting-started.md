---
title: "Getting Started"
component: "Splitter"
description: "Explains to get started with Splitter component with its key features such as resizable,validation and nested splitter, etc."
---
# Getting Started

The following section explains the steps required to create the Syncfusion's Angular Splitter component.
The Splitter component will make splittable layouts by placing separator in-between two panes. Based on the position of the separator you can adjust size of the splitter panes in the dynamic manner.

## Getting Started with Angular CLI

The following section explains the steps required to create and configure basic angular-cli application.

### Prerequisites

To get started with Syncfusion Angular UI Components, make sure that you have compatible versions of Angular and TypeScript.

* Angular : 4+
* TypeScript : 2.6+

### Setting up an Angular project

Angular provides an easiest way to setup project using Angular CLI [Angular CLI](https://github.com/angular/angular-cli) tool.

Install the CLI application globally in your machine.

```javascript

  npm install -g @angular/cli

```

### Create a new application

```javascript

  ng new syncfusion-angular-app

```

Once you have executed the above command you may ask for following options,
* Would you like to add Angular routing?
* Which stylesheet format would you like to use?

By default, it install the CSS style base application. To setup with SCSS, pass --style=SCSS argument on create project.

Example code snippet.

```javascript

  ng new syncfusion-angular-app --style=SCSS

```

Navigate to the created project folder.

```javascript

  cd syncfusion-angular-app

```

## Install Syncfusion Layouts package

Syncfusion packages are distributed in npm as `@syncfusion` scoped packages. You can get all the Angular Syncfusion package from npm [link](https://www.npmjs.com/search?q=%40syncfusion%2Fej2-angular-).

Add Syncfusion Angular Layouts package to use Splitter component in your application. By using following Command you can add required packages,

```javascript

npm install @syncfusion/ej2-angular-layouts --save
(or)
npm i @syncfusion/ej2-angular-layouts --save

```

## Adding Splitter module

Once you have successfully installed the layouts package, corresponding component modules are ready to configure in your application from the installed location. Syncfusion Angular package provides two different types of ngModules.

Refer to [Ng-Module](https://ej2.syncfusion.com/angular/documentation/common/ng-module/) to learn about `ngModules`.

Refer to the following snippet to import the `SplitterModule` in `app.module.ts` from the `@syncfusion/ej2-angular-layouts`.

```javascript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';

import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';
// Imported syncfusion SplitterModule from layouts package
import { SplitterModule } from '@syncfusion/ej2-angular-layouts';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    // Registering EJ2 Splitter Module
    SplitterModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }

```

## Adding Splitter component

Add the Splitter component snippet in `app.component.ts` as follows.

```typescript

import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <div id='container'>
      <ejs-splitter #horizontal height='110px' width='100%' >
          <e-panes>
            <e-pane></e-pane>
            <e-pane></e-pane>
          </e-panes>
      </ejs-splitter>
    </div>`
})
export class AppComponent {
    constructor() {
    }
}

```

Add following styles in corresponding css file. The below example contains styles in styles.css file,

```css

#container {
  margin: 50px auto;
}

```

## Adding CSS reference

The following CSS files are available in `../node_modules/@syncfusion` package folder. This can be referenced in [src/styles.css] using following code.

```css

      @import '../node_modules/@syncfusion/ej2-base/styles/material.css';
      @import '../node_modules/@syncfusion/ej2-icons/styles/material.css';
      @import '../node_modules/@syncfusion/ej2-buttons/styles/material.css';
      @import '../node_modules/@syncfusion/ej2-angular-layouts/styles/material.css';

```

> The [Custom Resource Generator (CRG)](https://crg.syncfusion.com/) is an online web tool, which can be used to generate the custom script and styles for a set of specific components.
> This web tool is useful to combine the required component scripts and styles in a single file.

## Load content to the pane

You can load the pane contents either as HTML element or string type
using [content](../api/splitter/panePropertiesModel/#content) property.

The below example shows how to load the content to panes by using `ng-template`.

For detailed information, refer to the [Pane Content](./pane-content/) section.

{% tab template="splitter/load-content", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
    <div id='container'>
         <ejs-splitter #horizontal height='250px' width='550px'>
            <e-panes>
                <e-pane>
                  <ng-template #content>
                    <div class="content">
                      <h3 class="h3">HTML</h3>
                      <div class="code-preview">
                        &lt;<span>!DOCTYPE html&gt;</span>
                        <div>&lt;<span>html&gt;</span></div>
                        <div>&lt;<span>body&gt;</span></div>
                        &lt;<span>div</span> id="custom-image"&gt;
                        <div style="margin-left: 5px">&lt;<span>img</span> src="src/albert.png"&gt;</div>
                        <div>&lt;<span>div</span>&gt;</div>
                        <div>&lt;<span>/body&gt;</span></div>
                        <div>&lt;<span>/html&gt;</span></div>
                      </div>
                    </div>
                  </ng-template>
                </e-pane>
                <e-pane>
                  <ng-template #content>
                  <div class="content">
                    <h3 class="h3">CSS</h3>
                    <div class="code-preview">
                    <span>img {{ '{' }}</span>
                    <div id="code-text">margin:<span>0 auto;</span></div>
                    <div id="code-text">display:<span>flex;</span></div>
                    <div id="code-text">height:<span>70px;</span></div>
                    <span>{{ '}' }}</span>
                    </div>
                  </div>
                  </ng-template>
                </e-pane>
                <e-pane>
                  <ng-template #content>
                      <div class="content">
                        <h3 class="h3">JavaScript</h3>
                        <div class="code-preview">
                        <span>var</span> image = document.getElementById("custom-image");
                        <div>image.addEventListener("click", function() {{ '{' }}</div>
                            <div style="padding-left: 20px;">// Code block for click action</div>
                            <span> {{ '}'}} </span>
                        </div>
                      </div>
                  </ng-template>
                </e-pane>
            </e-panes>
          </ejs-splitter>
        </div>`
})
export class AppComponent {
    constructor() {
    }
}

```

{% endtab %}

## Running the application

Run the `ng serve` command in command window, it will serve your application and you can open the browser window. Output will appear as follows.

{% tab template="splitter/getting-started",isDefaultActive=true, sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
    <div id='container'>
          <ejs-splitter #horizontal height='250px' width='600px'>
            <e-panes>
                <e-pane></e-pane>
                <e-pane></e-pane>
                <e-pane></e-pane>
            </e-panes>
          </ejs-splitter>
    </div>`
})
export class AppComponent {
    constructor() {
    }
}

```

{% endtab %}

## See Also

* [Construct different layouts using Splitter](./different-layouts)