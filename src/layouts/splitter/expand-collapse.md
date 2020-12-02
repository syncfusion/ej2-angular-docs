---
title: "Expand and Collapse"
component: "Splitter"
description: "This section explains about how to configure collapsible splitter panes, which helps to do expand and collapse action dynamically."
---

# Expand and Collapse

## Collapsible panes

The Splitter panes can be configured with built-in expand and collapse functionalities. By default, the collapsible behavior is disabled. Enable the [collapsible](../api/splitter/panePropertiesModel/#collapsible) behavior in the paneSettings property to show or hide the expand or collapse icons in the panes. You can dynamically expand and collapse the panes by clicking on the corresponding icons.

The following code shows how to enable collapsible behavior.

{% tab template="splitter/expand-collapse", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
      <div id='template_container'>
         <ejs-splitter #expand height='250px' width='580px' >
            <e-panes>
                <e-pane size='200px' [collapsible]='true'>
                    <ng-template #content>
                        <div class="template">
                            <h3>PARIS </h3>Paris, the city of lights and love - this short guide is full of ideas for how to make the most of the romanticism...
                        </div>
                    </ng-template>
                </e-pane>
                <e-pane size='200px' [collapsible]='true'>
                    <ng-template #content>
                        <div class="template">
                            <h3>CAMEMBERT </h3>The village in the Orne département of Normandy where the famous French cheese is originated from.
                        </div>
                    </ng-template>
                </e-pane>
                <e-pane size='200px' [collapsible]='true'>
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

## Programmatically control the expand and collapse action

The Splitter provides public method to control the expand and collapse behavior programmatically using the [expand](../api/splitter/#expand) and [collapse](../api/splitter/#collapse) methods. Refer to the following code example.

{% tab template="splitter/expand-collapse-method", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { SplitterComponent} from '@syncfusion/ej2-angular-layouts';

@Component({
    selector: 'app-root',
    template: `
      <div id='container'>
         <ejs-splitter #splitterInstance height='200px' width='600px'>
            <e-panes>
                <e-pane size='200px' [collapsible]='true' content='<div class="content" >Left pane</div>'>
                </e-pane>
                <e-pane size='200px' [collapsible]='true' content='<div class="content">Middle pane</div>'>
                </e-pane>
                <e-pane size='200px' [collapsible]='true' content='<div class="content">Right pane</div>'>
                </e-pane>
            </e-panes>
          </ejs-splitter>
          <button ejs-button id='expand' (click)="expandClick()">Expand</button>
          <button ejs-button id='collapse' (click)="collapseClick()">Collapse</button>
      </div>`
})
export class AppComponent {
    constructor() {
    }

    @ViewChild('splitterInstance') splitterObj: SplitterComponent;

    public expandClick: any = () => {
       this.splitterObj.collapse(0);
    }

    public collapseClick: any = () => {
       this.splitterObj.expand(0);
    }
}

```

{% endtab %}

## Specify initial state to panes

You can render specific panes with collapsed state on page load. Specify a Boolean value to the [collapsed](../api/splitter/#collapsed) property to control this behavior. The following code explains how to collapse panes on rendering (the second panes renders with collapsed state).

{% tab template="splitter/collapsed", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
      <div id='container'>
         <ejs-splitter #collapsed height='200px' width='600px'>
            <e-panes>
                <e-pane size='200px' [collapsible]='true' content='<div class="contents"><h3 class="h3">PARIS </h3>Paris, the city of lights and love - this short guide is full of ideas for how to make the most of the romanticism...</div>'>
                </e-pane>
                <e-pane [collapsible]='true' [collapsed]='true' size='200px' content='<div class="contents"><h3 class="h3">CAMEMBERT </h3>The village in the Orne département of Normandy where the famous French cheese is originated from.</div>'>
                </e-pane>
                <e-pane [collapsible]='true' size='200px' content='<div class="contents"><h3 class="h3">GRENOBLE </h3>The capital city of the French Alps and a major scientific center surrounded by many ski resorts, host of the Winter Olympics in 1968.</div>'>
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

* [Resizable split panes](./resize)