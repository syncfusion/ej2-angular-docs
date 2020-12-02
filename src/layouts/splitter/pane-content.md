---
title: "Pane Content"
component: "Splitter"
description: "This section explains how to provide plain text content or HTML markup or integrate other Angular UI controls as content of splitter."
---

# Pane Content

This section explains how to provide plain text content or HTML markup or integrate other Angular UI controls as content of Splitter.

## Template

You can render the HTML element directly to the Splitter pane content using ng-template.

{% tab template="splitter/template", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
      <div id='template_container'>
         <ejs-splitter #template height='250px' width='580px' >
            <e-panes>
                <e-pane size='200px'>
                    <ng-template #content>
                        <div class="template">
                            <h3>PARIS </h3>Paris, the city of lights and love - this short guide is full of ideas for how to make the most of the romanticism...
                        </div>
                    </ng-template>
                </e-pane>
                <e-pane size='200px'>
                    <ng-template #content>
                        <div class="template">
                            <h3>CAMEMBERT </h3>The village in the Orne département of Normandy where the famous French cheese is originated from.
                        </div>
                    </ng-template>
                </e-pane>
                <e-pane size='200px'>
                    <ng-template #content>
                        <div class="template">
                            <h3>GRENOBLE </h3>The capital city of the French Alps and a major scientific center surrounded by many ski resorts, host of the Winter Olympics in 1968.
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

## Angular UI Components

You can render any Angular UI components along with their native and control events within Splitter as pane content.

You can refer [Accordion within splitter](https://ej2.syncfusion.com/angular/demos/#/material/splitter/accordion-navigation-menu) and [Listview within splitter](https://ej2.syncfusion.com/angular/demos/#/material/splitter/details-view) samples.

## Plain content

You can add the plain text as a pane contents using either inner HTML or [content](../api/splitter/panePropertiesModel/#content) API

{% tab template="splitter/plain-content", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
      <div id='container'>
         <ejs-splitter #plain height='200px' width='600px'>
            <e-panes>
                <e-pane size='200px' content='<div class="content">Left pane</div>'>
                </e-pane>
                <e-pane size='200px' content='<div class="content">Middle pane</div>'>
                </e-pane>
                <e-pane size='200px' content='<div class="content">Right pane</div>'>
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

## HTML Markup

Splitter is a layout based container component. You can render the pane contents from existing HTML markup. Converting HTML markup as Splitter pane is easy way to add the panes content dynamically.

{% tab template="splitter/html-content", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
      <div id='container'>
         <ejs-splitter #markup height='200px' width='600px'>
            <e-panes>
                <e-pane size='200px' content='<div class="content"><h3 class="h3">PARIS </h3>Paris, the city of lights and love - this short guide is full of ideas for how to make the most of the romanticism...</div>'>
                </e-pane>
                <e-pane size='200px' content='<div class="content"><h3 class="h3">CAMEMBERT </h3>The village in the Orne département of Normandy where the famous French cheese is originated from.</div>'>
                </e-pane>
                <e-pane size='200px' content='<div class="content"><h3 class="h3">GRENOBLE </h3>The capital city of the French Alps and a major scientific center surrounded by many ski resorts, host of the Winter Olympics in 1968.</div>'>
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

## Pane content using selector

You can set HTML element as pane [content](../api/splitter/panePropertiesModel/#content) using the query selectors such as ID or CSS class selectors.

The following code demonstrates how to fetch an element from the document and load it to pane using its ID.

{% tab template="splitter/selector-content", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript

import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
      <div id='container'>
        <!-- render splitter component -->
        <ejs-splitter #horizontal height='200px' separatorSize=4 width='100%'></ejs-splitter>

        <!-- pane contents -->

        <div id="left-pane-content" style="display: none;">
        <div>Left pane<div id='panetext'>size: 25%</div>
        <div id='panetext'>min: 60px</div>
        </div>
        </div>

        <div id="middle-pane-content" style="display: none;">
        <span>Middle pane<div id="panetext">size: 50%</div>
        <div id="panetext">min: 60px</div>
        </span>
        </div>

        <div id="last-pane-content" style="display: none;">
        <span>Right pane<div id="panetext">size: 25%</div>
        <div id="panetext">min: 60px</div>
        </span>
        </div>
      </div>`
})
export class AppComponent {
    constructor() {
    }
    @ViewChild('horizontal') splitterObj: SplitterComponent;  
  ngAfterViewInit() {
    this.splitterObj.paneSettings = [
      { size: '25%', min: '60px', content: '#left-pane-content' },
      { size: '50%', min: '60px', content: '#middle-pane-content' },
      { size: '25%', min: '60px', content: '#last-pane-content' }]
  }
}

```

{% endtab %}