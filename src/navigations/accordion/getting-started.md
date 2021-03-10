---
title: "Accordion Getting Started"
component: "Accordion"
description: "This section explains how to create Accordion control in an Angular application with its basic features."
---

# Getting Started

This section briefly explains about how to create a simple **Accordion** and configure its available functionalities in Angular
using Angular quickstart.

## Dependencies

The following list of dependencies are required to use the Accordion component in your application.

```javascript
|-- @syncfusion/ej2-angular-navigations
    |-- @syncfusion/ej2-angular-base
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-navigations
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

## Adding Syncfusion Accordion package

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) registry.

To install Accordion component, use the following command.

```bash
npm install @syncfusion/ej2-angular-navigations --save
```

> The **--save** will instruct NPM to include the Accordion package inside of the **dependencies** section of the **package.json**.

## Registering Accordion Module

Import Accordion module into Angular application(app.module.ts) from the package **@syncfusion/ej2-angular-navigations** [src/app/app.module.ts].

```javascript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the AccordionModule for the Accordion component
import { AccordionModule } from '@syncfusion/ej2-angular-navigations';
import { AppComponent }  from './app.component';

@NgModule({
  //declaration of ej2-angular-navigations module into NgModule
  imports:      [ BrowserModule, AccordionModule ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## Adding CSS reference

The following CSS files are available in `../node_modules/@syncfusion` package folder.
This can be referenced in [src/styles.css] using following code.

```css
@import '../node_modules/@syncfusion/ej2-base/styles/material.css';  
@import '../node_modules/@syncfusion/ej2-buttons/styles/material.css';  
@import '../node_modules/@syncfusion/ej2-popups/styles/material.css';  
@import '../node_modules/@syncfusion/ej2-navigations/styles/material.css';

```

## Add Accordion component

Modify the template in [src/app/app.component.ts] file to render the accordion component.
Add the Angular Accordion by using `<ejs-accordion>` selector in **template** section of the app.component.ts file.

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-root',
  // specifies the template string for the Accordion component
  template: `<ejs-accordion> </ejs-accordion>`
})
export class AppComponent {

}

```

## Initialize the Accordion using Items

The Accordion can be rendered by defining an array of `items`.

```javascript
import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'my-app',
    template: `
       <ejs-accordion>
        <e-accordionitems>
          <e-accordionitem expanded='true'>
            <ng-template #header>
              <div>ASP.NET</div>
            </ng-template>
            <ng-template #content>
              <div>Microsoft ASP.NET is a set of technologies in the Microsoft .NET Framework for building Web applications and XML Web
                services. ASP.NET pages execute on the server and generate markup such as HTML, WML, or XML that is sent to a desktop
                or mobile browser. ASP.NET pages use a compiled,event-driven programming model that improves performance and enables
                the separation of application logic and user interface.</div>
            </ng-template>
          </e-accordionitem>
          <e-accordionitem>
            <ng-template #header>
              <div>ASP.NET MVC</div>
            </ng-template>
            <ng-template #content>
              <div>The Model-View-Controller (MVC) architectural pattern separates an application into three main components: the model,
                the view, and the controller. The ASP.NET MVC framework provides an alternative to the ASP.NET Web Forms pattern for
                creating Web applications. The ASP.NET MVC framework is a lightweight, highly testable presentation framework that
                (as with Web Forms-based applications) is integrated with existing ASP.NET features, such as master pages and membership-based
                authentication.
              </div>
            </ng-template>
          </e-accordionitem>
          <e-accordionitem>
            <ng-template #header>
              <div>JavaScript</div>
            </ng-template>
            <ng-template #content>
              <div>JavaScript (JS) is an interpreted computer programming language.It was originally implemented as part of web browsers
                so that client-side scripts could interact with the user, control the browser, communicate asynchronously, and alter
                the document content that was displayed.More recently, however, it has become common in both game development and
                the creation of desktop applications.</div>
            </ng-template>
          </e-accordionitem>
        </e-accordionitems>
    </ejs-accordion>
        `
})

export class AppComponent {

}
```

* Run the application in the browser using the following command.

```shell
npm start
```

The following code example depicts the way to initialize the Accordion on a single element.

Output will be as follows:

{% tab template="accordion/accordion", isDefaultActive=true, sourceFiles="app/**/*.ts"    %}

```typescript
import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-accordion>
        <e-accordionitems>
          <e-accordionitem expanded='true'>
            <ng-template #header>
              <div>ASP.NET</div>
            </ng-template>
            <ng-template #content>
              <div>Microsoft ASP.NET is a set of technologies in the Microsoft .NET Framework for building Web applications and XML Web
                services. ASP.NET pages execute on the server and generate markup such as HTML, WML, or XML that is sent to a desktop
                or mobile browser. ASP.NET pages use a compiled,event-driven programming model that improves performance and enables
                the separation of application logic and user interface.</div>
            </ng-template>
          </e-accordionitem>
          <e-accordionitem>
            <ng-template #header>
              <div>ASP.NET MVC</div>
            </ng-template>
            <ng-template #content>
              <div>The Model-View-Controller (MVC) architectural pattern separates an application into three main components: the model,
                the view, and the controller. The ASP.NET MVC framework provides an alternative to the ASP.NET Web Forms pattern for
                creating Web applications. The ASP.NET MVC framework is a lightweight, highly testable presentation framework that
                (as with Web Forms-based applications) is integrated with existing ASP.NET features, such as master pages and membership-based
                authentication.
              </div>
            </ng-template>
          </e-accordionitem>
          <e-accordionitem>
            <ng-template #header>
              <div>JavaScript</div>
            </ng-template>
            <ng-template #content>
              <div>JavaScript (JS) is an interpreted computer programming language.It was originally implemented as part of web browsers
                so that client-side scripts could interact with the user, control the browser, communicate asynchronously, and alter
                the document content that was displayed.More recently, however, it has become common in both game development and
                the creation of desktop applications.</div>
            </ng-template>
          </e-accordionitem>
        </e-accordionitems>
    </ejs-accordion>
        `
})

export class AppComponent {

}
```

{% endtab %}

## Initialize the Accordion using HTML elements

The Accordion component can be rendered based on the given HTML element using `<ejs-accordion>`.
You need to follow the below structure of HTML elements to render the Accordion inside the `<ejs-accordion>` tag.

```html
  <ejs-accordion>   --> Root Accordion Element
       <div>      --> Accordion Item Container
            <div>   --> Accordion Header Container
                <div> </div> --> Accordion Header
            </div>
            <div>  --> Accordion Panel Container
                <div> </div> --> Accordion Content
             </div>
        </div>
  </ejs-accordion>
```

{% tab template="accordion/accordion-container", sourceFiles="app/**/*.ts"    %}

```typescript
import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-accordion>
    <div>
        <div>
            <div> ASP.NET </div>
        </div>
        <div>
            <div> Microsoft ASP.NET is a set of technologies in the Microsoft .NET Framework for building Web applications
                  and XML Web services </div>
        </div>
    </div>
    <div>
        <div>
            <div> ASP.NET MVC </div>
        </div>
        <div>
            <div>The Model-View-Controller (MVC) architectural pattern separates an application into three main components:
                 the model, the view, and the controller </div>
        </div>
    </div>
    <div>
        <div>
            <div> JavaScript </div>
        </div>
        <div>
            <div>JavaScript (JS) is an interpreted computer programming language.It was originally implemented as part
                 of web browsers so that client-side scripts could interact with the user, control the browser </div>
        </div>
    </div>
</ejs-accordion>`
})

export class AppComponent {

}
```

{% endtab %}

> You can add the custom class into Accordion component using [`cssClass`](../api/accordion/accordionItem#cssclass) property which is used to customize the Accordion component.

## See Also

* [How to load accordion items dynamically](./how-to/load-accordion-items-dynamically/)