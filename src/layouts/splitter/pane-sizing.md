---
title: "Pane Sizing"
component: "Splitter"
description: "This section explains about user can feed pane sizes."
---

# Pane Sizing

Splitter allows you to provide pane sizes either in pixel or percentage formats.

`Pane size in pixel`

{% tab template="splitter/pane-sizes", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
      <div id='container'>
         <ejs-splitter #plain height='200px' width='600'>
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

`Pane size in percentage`

{% tab template="splitter/pane-sizes", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript

import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
      <div id='container'>
         <ejs-splitter #plain height='200px' width='600'>
            <e-panes>
                <e-pane size='30%' content='<div class="content">Left pane</div>'>
                </e-pane>
                <e-pane size='40%' content='<div class="content">Middle pane</div>'>
                </e-pane>
                <e-pane size='30%' content='<div class="content">Right pane</div>'>
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

## Auto-size panes

The splitter panes are automatically adjusted within its layout on resizing, while the size of panes are not specified. Because the panes are designed based on flex layout by default. When add/remove or show/hide the panes, the panes are auto aligned within its container.

{% tab template="splitter/template", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript

import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
      <div id='container'>
         <ejs-splitter #template height='200px'width='600px' >
            <e-panes>
                <e-pane>
                    <ng-template #content>
                        <div class="auto-size-content">
                            <h3 class="h3">Grid </h3>
                            The ASP.NET DataGrid control, or DataTable is a feature-rich control used to display data in a tabular format.
                        </div>
                    </ng-template>
                </e-pane>
                <e-pane>
                    <ng-template #content>
                        <div class="auto-size-content">
                            <h3 class="h3">Schedule </h3>
                            The ASP.NET Scheduler, a.k.a. event calendar, facilitates almost all calendar features, thus allowing users to manage their time efficiently
                        </div>
                    </ng-template>
                </e-pane>
                <e-pane>
                    <ng-template #content>
                        <div class="auto-size-content">
                            <h3 class="h3">Chart </h3>
                            ASP.NET charts, a well-crafted easy-to-use charting package, is used to add beautiful charts in web and mobile applications
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

## Fixed pane

You can render the split panes with fixed size for both horizontal and vertical mode. Even you provide fixed sizes to all panes, the splitter will consider last pane as flexible pane. Because, the splitter needs at least one pane as flexible pane always to adjust its remaining layout space.

{% tab template="splitter/fixed-pane", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript

import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
      <div id='container'>
         <ejs-splitter #resize height='200px' width='600'>
            <e-panes>
                <e-pane size='200px'>
                    <ng-template #content>
                        <div class="fixed-pane-content">
                            <h3 class="h3">Grid </h3>
                            The ASP.NET DataGrid control, or DataTable is a feature-rich control used to display data in a tabular format.
                        </div>
                    </ng-template>
                </e-pane>
                <e-pane size='200px'>
                    <ng-template #content>
                        <div class="fixed-pane-content">
                            <h3 class="h3">Schedule </h3>
                            The ASP.NET Scheduler, a.k.a. event calendar, facilitates almost all calendar features, thus allowing users to manage their time efficiently
                        </div>
                    </ng-template>
                </e-pane>
                <e-pane size='200px'>
                    <ng-template #content>
                        <div class="fixed-pane-content">
                            <h3 class="h3">Chart </h3>
                            ASP.NET charts, a well-crafted easy-to-use charting package, is used to add beautiful charts in web and mobile applications
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
