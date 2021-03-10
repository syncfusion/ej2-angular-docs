---
title: "Tab Getting Started"
component: "Tab"
description: "This section explains how to create a Tab control in an Angular application with its basic features."
---

# Getting Started

This section briefly explains about how to create a simple Tab using Angular by configuring the Tab header content.

## Dependencies

The following is the list of dependencies required to use the Tab component in your application.

```javascript

|-- @syncfusion/ej2-angular-navigations
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-angular-base
    |-- @syncfusion/ej2-navigations
        |-- @syncfusion/ej2-buttons
        |-- @syncfusion/ej2-popups

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

## Adding Syncfusion Tab package

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) registry.

To install Tab component, use the following command.

```bash
npm install @syncfusion/ej2-angular-navigations --save
```

> The **--save** will instruct NPM to include the Tab package inside of the **dependencies** section of the **package.json**.

## Registering Tab Module

Import Tab module into Angular application(app.module.ts) from the package **@syncfusion/ej2-angular-navigations** [src/app/app.module.ts].

```javascript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the TabModule for the Tab component
import { TabModule } from '@syncfusion/ej2-angular-navigations';
import { AppComponent }  from './app.component';

@NgModule({
  //declaration of ej2-angular-navigations module into NgModule
  imports:      [ BrowserModule, TabModule ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## Adding CSS reference

The following CSS files are available in `../node_modules/@syncfusion`package folder.
This can be referenced in [src/styles.css] using following code.

```css
@import '../node_modules/@syncfusion/ej2-base/styles/material.css';  
@import '../node_modules/@syncfusion/ej2-buttons/styles/material.css';  
@import '../node_modules/@syncfusion/ej2-popups/styles/material.css';  
@import '../node_modules/@syncfusion/ej2-navigations/styles/material.css';

```

## Add Tab component

Modify the template in [src/app/app.component.ts] file to render the tab component.
Add the Angular Tab by using `<ejs-tab>` selector in **template** section of the app.component.ts file.

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-root',
  // specifies the template string for the Tab component
  template: `<ejs-tab> </ejs-tab>`
})
export class AppComponent implements OnInit {

    ngOnInit(): void {
    }
}

```

## Initialize the Tab using JSON items collection

The Tab can be rendered by defining a JSON array. The item is rendered with header [`text`](../api/tab/header#text) and
[`content`](../../api/tab/tabItemModel#content) for each Tab.

```typescript

import { Component } from '@angular/core';
import { TabComponent } from '@syncfusion/ej2-angular-navigations';

/**
 * Adaptive Tab Component
 */

@Component({
    selector: 'app-container',
    template: `<ejs-tab id="element">
            <e-tabitems>
                <e-tabitem [header]='headerText[0]' [content]="content0"></e-tabitem>
                <e-tabitem [header]='headerText[1]' [content]="content1"></e-tabitem>
                <e-tabitem [header]='headerText[2]' [content]="content2"></e-tabitem>
            </e-tabitems>
        </ejs-tab>`

})
export class AppComponent {

       public headerText: Object = [{ 'text': 'Twitter' }, { 'text': 'Facebook' },{ 'text': 'WhatsApp' }];

       public content0: string = 'Twitter is an online social networking service that enables users to send and read short 140-character ' +
            'messages called "tweets". Registered users can read and post tweets, but those who are unregistered can only read ' +
            'them. Users access Twitter through the website interface, SMS or mobile device app Twitter Inc. is based in San ' +
            'Francisco and has more than 25 offices around the world. Twitter was created in March 2006 by Jack Dorsey, ' +
            'Evan Williams, Biz Stone, and Noah Glass and launched in July 2006. The service rapidly gained worldwide popularity, ' +
            'with more than 100 million users posting 340 million tweets a day in 2012.The service also handled 1.6 billion ' +
            'search queries per day.';

    public content1: string = 'Facebook is an online social networking service headquartered in Menlo Park, California. Its website was ' +
            'launched on February 4, 2004, by Mark Zuckerberg with his Harvard College roommates and fellow students Eduardo ' +
            'Saverin, Andrew McCollum, Dustin Moskovitz and Chris Hughes.The founders had initially limited the website\'\s ' +
            'membership to Harvard students, but later expanded it to colleges in the Boston area, the Ivy League, and Stanford ' +
            'University. It gradually added support for students at various other universities and later to high-school students.';

    public content2: string = 'WhatsApp Messenger is a proprietary cross-platform instant messaging client for smartphones that operates ' +
            'under a subscription business model. It uses the Internet to send text messages, images, video, user location and ' +
            'audio media messages to other users using standard cellular mobile numbers. As of February 2016, WhatsApp had a user ' +
            'base of up to one billion,[10] making it the most globally popular messaging application. WhatsApp Inc., based in ' +
            'Mountain View, California, was acquired by Facebook Inc. on February 19, 2014, for approximately US$19.3 billion.';


}

```

## Run the application

After completing the configuration required to render a basic Tab, run the following command to
display the output in your default browser.

```shell
npm start
```

The following example illustrates the output in your browser.

{% tab template="tab/basic", isDefaultActive=true, sourceFiles="app/**/*.ts,index.html"%}

```typescript

import { Component } from '@angular/core';
import { TabComponent } from '@syncfusion/ej2-angular-navigations';

/**
 * Tab Component
 */

@Component({
    selector: 'app-container',
    template: `<ejs-tab id="element">
            <e-tabitems>
                <e-tabitem [header]='headerText[0]' [content]="content0"></e-tabitem>
                <e-tabitem [header]='headerText[1]' [content]="content1"></e-tabitem>
                <e-tabitem [header]='headerText[2]' [content]="content2"></e-tabitem>
            </e-tabitems>
        </ejs-tab>`
})
export class AppComponent {
    public headerText: Object = [{ 'text': 'Twitter' }, { 'text': 'Facebook' },{ 'text': 'WhatsApp' }];

    public content0: string = 'Twitter is an online social networking service that enables users to send and read short 140-character ' +
            'messages called "tweets". Registered users can read and post tweets, but those who are unregistered can only read ' +
            'them. Users access Twitter through the website interface, SMS or mobile device app Twitter Inc. is based in San ' +
            'Francisco and has more than 25 offices around the world. Twitter was created in March 2006 by Jack Dorsey, ' +
            'Evan Williams, Biz Stone, and Noah Glass and launched in July 2006. The service rapidly gained worldwide popularity, ' +
            'with more than 100 million users posting 340 million tweets a day in 2012.The service also handled 1.6 billion ' +
            'search queries per day.';

    public content1: string = 'Facebook is an online social networking service headquartered in Menlo Park, California. Its website was ' +
            'launched on February 4, 2004, by Mark Zuckerberg with his Harvard College roommates and fellow students Eduardo ' +
            'Saverin, Andrew McCollum, Dustin Moskovitz and Chris Hughes.The founders had initially limited the website\'\s ' +
            'membership to Harvard students, but later expanded it to colleges in the Boston area, the Ivy League, and Stanford ' +
            'University. It gradually added support for students at various other universities and later to high-school students.';

    public content2: string = 'WhatsApp Messenger is a proprietary cross-platform instant messaging client for smartphones that operates ' +
            'under a subscription business model. It uses the Internet to send text messages, images, video, user location and ' +
            'audio media messages to other users using standard cellular mobile numbers. As of February 2016, WhatsApp had a user ' +
            'base of up to one billion,[10] making it the most globally popular messaging application. WhatsApp Inc., based in ' +
            'Mountain View, California, was acquired by Facebook Inc. on February 19, 2014, for approximately US$19.3 billion.';
}

```

{% endtab %}

> In the above sample code, `#element` is the `id` of the HTML element in a page to which the Tab is initialized.

## Initialize the Tab using template

The Tab component can also be rendered using the Angular template `ng-template`. The Tab consists this template support for both its header and content of the item property.
You need to follow the below structure of `ng-template` to render the Tab,

```html

  <ejs-tab id="element">
    <e-tabitems>
        <e-tabitem>
            <ng-template #headerText>   --> Tab header
                <div>   --> Header Item
                </div>
            </ng-template>
            <ng-template #content>      --> Tab content
                        --> Content Item
            </ng-template>
        </e-tabitem>
    </e-tabitems>
  </ejs-tab>

```

{% tab template="tab/basic", isDefaultActive=true, sourceFiles="app/**/*.ts,index.html"%}

```typescript

import { Component } from '@angular/core';
import { TabComponent } from '@syncfusion/ej2-angular-navigations';

/**
 * Adaptive Tab Component
 */

@Component({
    selector: 'app-container',
    template: `<ejs-tab id="element">
            <e-tabitems>
                    <e-tabitem>
                        <ng-template #headerText>
                           <div> Twitter </div>
                        </ng-template>
                        <ng-template #content>
                            Twitter is an online social networking service that enables users to send and read short 140-character messages called "tweets".
                            Registered users can read and post tweets, but those who are unregistered can only read them. Users access Twitter
                            through the website interface, SMS or mobile device app Twitter Inc. is based in San Francisco and has more than 25
                            offices around the world. Twitter was created in March 2006 by Jack Dorsey, Evan Williams, Biz Stone, and Noah Glass
                            and launched in July 2006. The service rapidly gained worldwide popularity, with more than 100 million users posting
                            340 million tweets a day in 2012.The service also handled 1.6 billion search queries per day.
                        </ng-template>
                    </e-tabitem>
                    <e-tabitem>
                        <ng-template #headerText>
                           <div> Facebook </div>
                        </ng-template>
                        <ng-template #content>
                            Facebook is an online social networking service headquartered in Menlo Park, California. Its website was launched on February
                            4, 2004, by Mark Zuckerberg with his Harvard College roommates and fellow students Eduardo Saverin, Andrew McCollum,
                            Dustin Moskovitz and Chris Hughes.The founders had initially limited the website\'\s membership to Harvard students,
                            but later expanded it to colleges in the Boston area, the Ivy League, and Stanford University. It gradually added support
                            for students at various other universities and later to high-school students.
                        </ng-template>
                    </e-tabitem>
                    <e-tabitem>
                        <ng-template #headerText>
                           <div> WhatsApp </div>
                        </ng-template>
                        <ng-template #content>
                            WhatsApp Messenger is a proprietary cross-platform instant messaging client for smartphones that operates under a subscription
                            business model. It uses the Internet to send text messages, images, video, user location and audio media messages to
                            other users using standard cellular mobile numbers. As of February 2016, WhatsApp had a user base of up to one billion,[10]
                            making it the most globally popular messaging application. WhatsApp Inc., based in Mountain View, California, was acquired
                            by Facebook Inc. on February 19, 2014, for approximately US$19.3 billion.
                        </ng-template>
                    </e-tabitem>
                </e-tabitems>
            </ejs-tab>`
})
export class AppComponent {
  
}

```

{% endtab %}

## Initialize the Tab using HTML elements

The Tab component can be rendered based on the given HTML element using `<ejs-tab>` tag.
Header section must be enclosed with in a wrapper element using `e-tab-header` class and corresponding content must be mapped with `e-content` class.
You need to follow the below structure of HTML elements to render the Tab,

```html

  <ejs-tab id="element">   --> Root Tab element
    <div class="e-tab-header">      --> Tab header
       <div>   --> Header Item
       </div>
    </div>
    <div class="e-content">      --> Tab content
       <div>   --> Content Item
       </div>
    </div>
  </ejs-tab>

```

{% tab template="tab/tab-container", sourceFiles="app/**/*.ts,index.html"%}

```typescript

import { Component } from '@angular/core';
import { TabComponent } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-container',
        template: `<ejs-tab id="element">
            <div class="e-tab-header">
                <div>Twitter </div>
                <div>Facebook </div>
                <div>WhatsApp </div>
            </div>
            <div class="e-content">
                <div>
                        Twitter is an online social networking service that enables users to send and read short 140-character messages called 'tweets'. Registered users can read and post tweets, but those who are unregistered can only read them. Users access Twitter through the website interface, SMS or mobile device app Twitter Inc. is based in San Francisco and has more than 25 offices around the world. Twitter was created in March 2006 by Jack Dorsey, Evan Williams, Biz Stone, and Noah Glass and launched in July 2006. The service rapidly gained worldwide popularity, with more than 100 million users posting 340 million tweets a day in 2012.The service also handled 1.6 billion search queries per day.
                </div>
                <div>
                        Facebook is an online social networking service headquartered in Menlo Park, California. Its website was launched on February 4, 2004, by Mark Zuckerberg with his Harvard College roommates and fellow students Eduardo Saverin, Andrew McCollum, Dustin Moskovitz and Chris Hughes.The founders had initially limited the website's membership to Harvard students, but later expanded it to colleges in the Boston area, the Ivy League, and Stanford University. It gradually added support for students at various other universities and later to high-school students.
                </div>
                <div>
                        WhatsApp Messenger is a proprietary cross-platform instant messaging client for smartphones that operates under a subscription business model. It uses the Internet to send text messages, images, video, user location and audio media messages to other users using standard cellular mobile numbers. As of February 2016, WhatsApp had a user base of up to one billion,[10] making it the most globally popular messaging application. WhatsApp Inc., based in Mountain View, California, was acquired by Facebook Inc. on February 19, 2014, for approximately US$19.3 billion.
                </div>
            </div>
        </ejs-tab>`
})
export class AppComponent {
}

```

{% endtab %}

## See Also

* [How to load tab with DataSource](./how-to/load-tab-with-data-source/)