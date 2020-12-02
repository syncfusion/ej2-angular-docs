---
title: "Getting Started For Tooltip"
component: "Tooltip"
description: "Getting started with Tooltip component."
---

# Getting Started

This section briefly explains how to create a simple **Tooltip** component and configure its available functionalities in angular.

## Dependencies

The following list of dependencies are required to use Tooltip component in your application.

```javascript
|-- @syncfusion/ej2-angular-popups
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-angular-base
    |-- @syncfusion/ej2-popups
        |-- @syncfusion/ej2-buttons
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

## Adding Syncfusion Tooltip package

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) registry.

To install Tooltip component, use the following command.

```cmd
npm install @syncfusion/ej2-angular-popups --save
```

> The **--save** will instruct NPM to include the tooltip package inside of the `dependencies` section of the `package.json`.

## Registering Tooltip Module

* Import Tooltip module into Angular application(app.module.ts) from the package
`@syncfusion/ej2-angular-popups`.

```javascript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';

//Syncfusion ej2-angular-popups module
import { TooltipModule } from '@syncfusion/ej2-angular-popups';

import { AppComponent }  from './app.component';

@NgModule({
  imports:      [ BrowserModule, TooltipModule ], //declaration of TooltipModule module into NgModule
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## Adding CSS Reference

* Add Tooltip component's styles as given below in `styles.css`.

`[style.css]`

```css
@import "../node_modules/@syncfusion/ej2-base/styles/material.css";
@import "../node_modules/@syncfusion/ej2-angular-buttons/styles/material.css";
@import "../node_modules/@syncfusion/ej2-angular-popups/styles/material.css";
```

> We can also use [CRG](https://crg.syncfusion.com/) to generate combined component styles.

## Add Tooltip component

Modify the template in `app.component.ts` file to render the `Tooltip` component. Add the Angular Tooltip by using `<ejs-tooltip>` selector in `template` section of the app.component.ts file.

```javascript
import { Component, ViewEncapsulation } from '@angular/core';

@Component({
  selector: 'my-app',
  template: `
        <ejs-tooltip id='tooltip' content='Tooltip content'>
            Hover Me
        </ejs-tooltip>`,
  encapsulation: ViewEncapsulation.None
})
export class AppComponent  { }
```

## Run the application

* Now, run the application in the browser using the following command.

```shell
ng serve --open
```

The following code example depicts the way to initialize Tooltip on a single element.

{% tab template="tooltip/getting-started", isDefaultActive=true, sourceFiles="app/**/*.ts"  %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';

@Component({
  selector: 'my-app',
  template: `
    <div id='container' style="display: inline-block; position: relative; left: 50%;top: 100px;transform: translateX(-50%);">
        <ejs-tooltip id='tooltip' content='Tooltip content' target="#target">
            <button ejs-button id="target">Show Tooltip</button>
        </ejs-tooltip>
    </div>`,
  encapsulation: ViewEncapsulation.None
})
export class AppComponent  { }
```

{% endtab %}

### Initialize Tooltip within a container

It is possible to create Tooltip on multiple targets within a container. To do so, define the `selector` property with specific target
 elements - so that the tooltip will be initialized only on those matched targets within a container. In this case, the Tooltip content
  gets assigned from the `title` attribute of the target element.

Refer the following code example, to create a Tooltip on multiple targets within a container.

{% tab template="tooltip/getting-started", isDefaultActive=true, sourceFiles="app/**/*.ts,index.css"  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'my-app',
    template: `
        <div id="tool">
          <ejs-tooltip target='.e-info' position='RightCenter'>
            <form id="details" role="form">
              <table>
                <tr>
                    <td class="info">User Name</td>
                    <td>
                        <input type="text" class="e-info" name="firstname" title="Please enter your name"> </td>
                </tr>
                <tr>
                    <td class="info">Email Address</td>
                    <td>
                        <input type="text" class="e-info" name="email" title="Enter a valid email address">
                    </td>
                </tr>
                <tr>
                    <td class="info">Password</td>
                    <td>
                        <input type="password" class="e-info" name="password" title="Be at least 8 characters length">
                    </td>
                </tr>
                <tr>
                    <td class="info">Confirm Password</td>
                    <td>
                        <input type="password" class="e-info" name="Cpwd" title="Re-enter your password">
                    </td>
                </tr>
                <tr>
                    <td><input ejs-button id="sample" class="center" type="submit" value="Submit"></td>
                    <td><input ejs-button id="clear" class="center" type="reset" value="Reset"></td>
                </tr>
              </table>
            </form>
          </ejs-tooltip>
        </div>
        `,
})

export class AppComponent { }
```

{% endtab %}

> In the above sample, `details` refers to the container's id, and the target `.e-info` refers to the target elements available
> within that container.

## See Also

[Positioning Tooltip](./position)

[Tooltip Open Mode](./open-mode)

[Customize the Tooltip](./customization)
