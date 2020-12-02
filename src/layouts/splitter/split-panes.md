---
title: "Split Panes"
component: "Splitter"
description: "This section explain about split panes behaviours."
---

# Split Panes

This section explain about split panes behaviours.

## Horizontal layout

By default, Splitter will render in horizontal orientation. Splitter container will be split as panes in horizontal flow direction with vertical separator.

{% tab template="splitter/horizontal", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
      <div id='container'>
         <ejs-splitter #horizontal height='250px' width='600px'>
            <e-panes>
                <e-pane size='200px'>
                    <ng-template #content>
                        <div class="content">
                            <h3 class="h3">Grid </h3>
                            The ASP.NET DataGrid control, or DataTable is a feature-rich control used to display data in a tabular format.
                        </div>
                    </ng-template>
                </e-pane>
                <e-pane size='200px'>
                    <ng-template #content>
                        <div class="content">
                            <h3 class="h3">Schedule </h3>
                            The ASP.NET Scheduler, a.k.a. event calendar, facilitates almost all calendar features, thus allowing users to manage their time efficiently
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

## Vertical layout

By setting [orientation](../api/splitter/#orientation) property as `Vertical`, Splitter will render in vertical orientation. Splitter container will be split as panes in vertical flow direction with horizontal separator.

{% tab template="splitter/vertical", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
      <div id='container'>
         <ejs-splitter #vertical orientation='Vertical' height='305px' width='600px'>
            <e-panes>
                <e-pane size='100px'>
                    <ng-template #content>
                        <div class="content">
                            <h3 class="h3">Grid </h3>
                            The ASP.NET DataGrid control, or DataTable is a feature-rich control used to display data in a tabular format.
                        </div>
                    </ng-template>
                </e-pane>
                <e-pane size='100px'>
                    <ng-template #content>
                        <div class="content">
                            <h3 class="h3">Schedule </h3>
                            The ASP.NET Scheduler, a.k.a. event calendar, facilitates almost all calendar features, thus allowing users to manage their time efficiently
                        </div>
                    </ng-template>
                </e-pane>
                <e-pane size='100px'>
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

## Multiple panes

You can render the multiple panes with both `Horizontal` and `Vertical` orientations.

{% tab template="splitter/multiple", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
      <div id='container'>
         <ejs-splitter #multiple height='300px' width='600px'>
            <e-panes>
                <e-pane size='150px'>
                    <ng-template #content>
                        <div class="content">
                            <h3 class="h3">PARIS </h3>
                             Paris, the city of lights and love - this short guide is full of ideas for how to make the most of the romanticism...
                        </div>
                    </ng-template>
                </e-pane>
                <e-pane size='150px'>
                    <ng-template #content>
                        <div class="content">
                            <h3 class="h3">CAMEMBERT </h3>
                            The village in the Orne département of Normandy where the famous French cheese is originated from.
                        </div>
                    </ng-template>
                </e-pane>
                <e-pane size='150px'>
                    <ng-template #content>
                        <div class="content">
                            <h3 class="h3">GRENOBLE </h3>
                            The capital city of the French Alps and a major scientific center surrounded by many ski resorts, host of the Winter Olympics in 1968.
                        </div>
                    </ng-template>
                </e-pane>
                <e-pane size='150px'>
                    <ng-template #content>
                        <div class="content">
                            <h3 class="h3">Australia </h3>
                            Australia is a country and continent surrounded by the Indian and Pacific oceans. Its major cities – Sydney, Brisbane, Melbourne, Perth, Adelaide – are coastal. Its capital, Canberra, is inland.
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

## Separator

By default, pane separator will be render with `1px` width/height. You can customize the separator size by using [separatorSize](../api/splitter/#separatorsize) property.

> For Horizontal orientation, it will be considered as separator width.
> For Vertical orientation, it will be considered as separator height.

{% tab template="splitter/separator", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
      <div id='container'>
         <ejs-splitter #separator height='250px' separatorSize='5' width='600px'>
            <e-panes>
                <e-pane size='200px'>
                    <ng-template #content>
                        <div class="content">
                            <h3 class="h3">Grid </h3>
                            The ASP.NET DataGrid control, or DataTable is a feature-rich control used to display data in a tabular format.
                        </div>
                    </ng-template>
                </e-pane>
                <e-pane size='200px'>
                    <ng-template #content>
                        <div class="content">
                            <h3 class="h3">Schedule </h3>
                            The ASP.NET Scheduler, a.k.a. event calendar, facilitates almost all calendar features, thus allowing users to manage their time efficiently
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

## Nested Splitter

Splitter provides support to render the nested pane to achieve the complex layouts. You can use the same `<div>` element for splitter pane and nested splitter.

> Also you can render the nested splitter using direct child of the splitter pane. For this, nested splitter should have `100%` width and height to match with the parent pane dimensions.

{% tab template="splitter/nested", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { SplitterComponent} from '@syncfusion/ej2-angular-layouts';
import { Splitter } from '@syncfusion/ej2-layouts';

@Component({
    selector: 'app-root',
    template: `
        <div id='container'>
            <ejs-splitter #splitterInstance  id="nested-splitter" (created)='onCreated()' height='320px' width='580px'>
            <e-panes>
                <e-pane size='200px'>
                    <ng-template #content>
                        <div class="content">
                            <h3 class="h3">PARIS </h3>
                            Paris, the city of lights and love - this short guide is full of ideas for how to make the most of the romanticism...
                        </div>
                    </ng-template>
                </e-pane>
                <e-pane size= '200px'>
                    <ng-template #content>
                        <div class="content">
                            <h3 class="h3">CAMEMBERT </h3>
                            The village in the Orne département of Normandy where the famous French cheese is originated from.
                        </div>
                    </ng-template>
                </e-pane>
                <e-pane>
                    <ng-template #content>
                        <div id ='vertical_splitter' class="vertical_splitter">
                            <div>
                                <div class="content">
                                    <h3 class="h3">GRENOBLE </h3>
                                    The capital city of the French Alps and a major scientific center surrounded by many ski resorts, host of the Winter Olympics in 1968.
                                </div>
                            </div>
                            <div>
                                <div class="content">
                                    <h3 class="h3">Australia </h3>
                                    Australia is a country and continent surrounded by the Indian and Pacific oceans
                                </div>
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

    @ViewChild('splitterInstance') splitterObj: SplitterComponent;
    public onCreated () {
        let splitterObj1 = new Splitter({
            height: '310px',
            paneSettings: [
                { size: '150px', min: '20%'},
                { size: '100px', min: '20%'}
            ],
            orientation: 'Vertical'
        });
        splitterObj1.appendTo('#vertical_splitter');
    }
}

```

{% endtab %}

## Add or remove pane

You can add or remove panes programmatically to the splitter, By using
 [addPane](../api/splitter#addpane) and [removePane](../api/splitter#removepane) methods.

### Add pane

You can add the panes dynamically in the splitter by passing
[pane properties](https://ej2.syncfusion.com/documentation/api/splitter/panePropertiesModel/) along with index to the addPane method.

{% tab template="splitter/add-pane", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { SplitterComponent, PanePropertiesModel } from '@syncfusion/ej2-angular-layouts';

@Component({
    selector: 'app-root',
    template: `
      <div id='container'>
         <ejs-splitter #add height='200px' width='600px'>
            <e-panes>
                <e-pane size='150px'>
                    <ng-template #content>
                        <div class="content">Pane 1</div>
                    </ng-template>
                </e-pane>
                <e-pane size='150px'>
                    <ng-template #content>
                        <div class="content">Pane 2</div>
                    </ng-template>
                </e-pane>
            </e-panes>
          </ejs-splitter>
          <div id='addButton'>
            <button class='e-control e-btn' id='add' (click)='addPane()'>Add pane</button>
          </div>
      </div>`
})
export class AppComponent {
  @ViewChild('add') splitterObj: SplitterComponent;
    constructor() {
    }
    public paneDetails: PanePropertiesModel = {
        size: '190px',
        content: 'New Pane',
        min: '30px',
        max: '250px',
    }
    addPane(): void {
      if (this.splitterObj.allPanes.length >= 1) {
          this.splitterObj.addPane(this.paneDetails, 1);
      }
    }
}

```

{% endtab %}

### Remove pane

You can remove the split panes dynamically by passing the pane index to [removePane](../api/splitter#removepane) method.

{% tab template="splitter/remove-pane", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { SplitterComponent} from '@syncfusion/ej2-angular-layouts';

@Component({
    selector: 'app-root',
    template: `
      <div id='container'>
         <ejs-splitter #remove height='200px' width='600px'>
            <e-panes>
                <e-pane size='200px'>
                    <ng-template #content>
                        <div class="content">Pane 1</div>
                    </ng-template>
                </e-pane>
                <e-pane size='200px'>
                    <ng-template #content>
                        <div class="content">Pane 2</div>
                    </ng-template>
                </e-pane>
                <e-pane size='200px'>
                    <ng-template #content>
                        <div class="content">Pane 3</div>
                    </ng-template>
                </e-pane>
            </e-panes>
          </ejs-splitter>
          <div id='removeButton'>
            <button class='e-control e-btn' id='remove' (click)='removePane()'>Remove pane</button>
          </div>
      </div>`
})
export class AppComponent {
  @ViewChild('remove') splitterObj: SplitterComponent;
    constructor() {
    }

    removePane(): void {
      if (this.splitterObj.allPanes.length > 1) {
          this.splitterObj.removePane(1);
      }
    }
}

```

{% endtab %}

## See Also

* [Resizable split panes](./resize)
* [Collapsible panes](./expand-collapse)
* [Define size to a panes](./pane-sizing)
* [Specify content to a panes](./pane-content)