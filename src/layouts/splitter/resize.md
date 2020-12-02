---
title: "Resize"
component: "Splitter"
description: "This section explain about split panes resizing behaviors."
---

# Resize

By default, resizing will be enable for split panes. Resizing gripper element will be add to the separator to makes the resize easy.

> Horizontal Splitter will allows to resize in horizontal directions.
> Vertical Splitter will allows to resize in vertical directions.

While resizing, previous and next panes will be adjust its dimensions automatically.

## Min and Max validation

Splitter allows you to set the minimum and maximum sizes for each pane. Resizing will not be occur over the minimum and maximum values.

{% tab template="splitter/validation", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
      <div id='container'>
         <ejs-splitter #validate height='200px' width='600'>
            <e-panes>
                <e-pane size='200px' min='20%' max='40%'>
                    <ng-template #content>
                        <div class="content">
                            <h3 class="h3">Grid </h3>
                            The ASP.NET DataGrid control, or DataTable is a feature-rich control used to
                            display data in a tabular format.
                        </div>
                    </ng-template>
                </e-pane>
                <e-pane size='200px' min='30%' max='60%'>
                    <ng-template #content>
                        <div class="content">
                            <h3 class="h3">Schedule </h3>
                            The ASP.NET Scheduler, a.k.a. event calendar, facilitates almost all calendar features, thus allowing users to manage their time efficiently.
                        </div>
                    </ng-template>
                </e-pane>
                <e-pane size='200px'>
                    <ng-template #content>
                        <div class="content">
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

## Prevent resizing

You can disable the resizing for the pane by setting `false` to
the [resizable](../api/splitter/panePropertiesModel/#resizable) property within paneSettings.

{% tab template="splitter/fixed-pane", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
      <div id='container'>
         <ejs-splitter #resize height='200px' width='600'>
            <e-panes>
                <e-pane size='200px' min='20%' max='40%' [resizable]='false'>
                    <ng-template #content>
                        <div class="content">
                            <h3 class="h3">Grid </h3>
                            The ASP.NET DataGrid control, or DataTable is a feature-rich control used to
                            display data in a tabular format.
                        </div>
                    </ng-template>
                </e-pane>
                <e-pane size='200px' min='30%' max='60%'>
                    <ng-template #content>
                        <div class="content">
                            <h3 class="h3">Schedule </h3>
                            The ASP.NET Scheduler, a.k.a. event calendar, facilitates almost all calendar features, thus allowing users to manage their time efficiently.
                        </div>
                    </ng-template>
                </e-pane>
                <e-pane size='200px'>
                    <ng-template #content>
                        <div class="content">
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

> Note: Splitter resizing will be enabled only when the target of the adjacent pane's `resizable` api is also in `true` state.

## Refresh content on resizing

While resizing the panes, you can refresh the pane contents by using either [resizeStart](../api/splitter#resizestart),
[resizing](../api/splitter#resizestart) or [resizeStop](../api/splitter#resizestart) events.

## Customize Resize-gripper and Cursor

You can customize the resize gripper icon and cursor in CSS level.

{% tab template="splitter/grip-customization", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
      <div id='container'>
         <ejs-splitter #resizegrip id='resizegrip' height='200px' width='600'>
            <e-panes>
                <e-pane size='200px' min='20%' max='40%'>
                    <ng-template #content>
                        <div class="content">
                            <h3 class="h3">PARIS </h3>
                            Paris, the city of lights and love - this short guide is full of ideas for how to make the most of the romanticism...
                        </div>
                    </ng-template>
                </e-pane>
                <e-pane size='200px' min='30%' max='60%'>
                    <ng-template #content>
                        <div class="content">
                            <h3 class="h3">CAMEMBERT </h3>
                            The village in the Orne département of Normandy where the famous French cheese is originated from.
                        </div>
                    </ng-template>
                </e-pane>
                <e-pane size='200px'>
                    <ng-template #content>
                        <div class="content">
                            <h3 class="h3">GRENOBLE </h3>
                            The capital city of the French Alps and a major scientific center surrounded by many ski resorts, host of the Winter Olympics in 1968.
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

## See Also

* [Collapsible panes](./expand-collapse)