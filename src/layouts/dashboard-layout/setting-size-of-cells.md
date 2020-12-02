---
title: "Setting size of cells"
component: "DashboardLayout"
description: "This section explains how to adjust the size of the cells of Essential JS 2 DashboardLayout component"
---

# Configuring the layout

The entire layout dimensions are assigned based on the height and width of the parent element. Hence, a responsive or static layout can be created by assigning a percentage or static dimension values to the parent element. The layout adapts to mobile resolutions by transforming the entire layout into a stacked orientation, so that, the panels will be displayed in a vertical column.

The **Dashboard Layout** is a grid structured component which can be split into subsections of equal size known as cells. The total number of cells in each row is defined by using the `columns` property of the component. The width of each cell will be auto calculated based on the total number of cells placed in a row and the height of a cell will be same as that of its width. However, the height of these cells can also be configured to any desired size using the `cellAspectRatio` property (cellwidth/cellheight ratio) which defines the cell width to height ratio.

The number of rows within the layout has no limits and can have any number of rows based on the panels count and position. Panels which acts as data containers will be placed or positioned over these cells.

## Modifying cell size

In a dashboard, the data to be held by the panel in a cell may be of different size, hence different cell dimensions may be required in different scenarios. In this case, the size of these grid cells can be modified to the required size using the `columns` and `cellAspectRatio` properties.

The following sample demonstrates how to modify a cell size using the `columns` and `cellAspectRatio` properties. In the following sample, the width of the parent element is divided into 5 equal cells based on the columns property value resulting the width of each cell as 100px. The height of these cells will be 50px based on the cellAspectRatio value 100/50 (i.e., for every 100px of width, 50px will be the height of the cell).

{% tab template="dashboard-layout/modifying-cell-size", sourceFiles="app/app.component.ts,app/app.template.html,app/app.module.ts,app/main.ts,app/default-style.css" %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';

@Component({
    selector: 'app-root',
    styleUrls: ['app/default-style.css'],
    templateUrl: 'app/app.template.html',
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    public cellSpacing: number[] = [10, 10];
    public cellAspectRatio: number = 100/50;
    public panels: any = [{ "sizeX": 1, "sizeY": 1, "row": 0, "col": 0, content:'<div class="content">0</div>' },
    { "sizeX": 3, "sizeY": 2, "row": 0, "col": 1, content:'<div class="content">1</div>' },
    { "sizeX": 1, "sizeY": 3, "row": 0, "col": 4, content:'<div class="content">2</div>' },
    { "sizeX": 1, "sizeY": 1, "row": 1, "col": 0, content:'<div class="content">3</div>' },
    { "sizeX": 2, "sizeY": 1, "row": 2, "col": 0, content:'<div class="content">4</div>' },
    { "sizeX": 1, "sizeY": 1, "row": 2, "col": 2, content:'<div class="content">5</div>' },
    { "sizeX": 1, "sizeY": 1, "row": 2, "col": 3, content:'<div class="content">6</div>' }
    ];
}
```

{% endtab %}

## Setting cell spacing

The spacing between each panel in a row and column can be defined using the `cellSpacing` property. Adding spacing between the panels will make the layout effective and provides a clear data representation.

The following sample demonstrates the usage of the `cellSpacing` property, which helps in a neat and clear representation of a data.

{% tab template="dashboard-layout/setting-cell-spacing", sourceFiles="app/app.component.ts,app/app.template.html,app/app.module.ts,app/main.ts,app/default-style.css" %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';

@Component({
    selector: 'app-root',
    styleUrls: ['app/default-style.css'],
    templateUrl: 'app/app.template.html',
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    public cellSpacing: number[] = [20, 20];
    public panels: any = [{ "sizeX": 1, "sizeY": 1, "row": 0, "col": 0, content:'<div class="content">0</div>' },
    { "sizeX": 3, "sizeY": 2, "row": 0, "col": 1, content:'<div class="content">1</div>' },
    { "sizeX": 1, "sizeY": 3, "row": 0, "col": 4, content:'<div class="content">2</div>' },
    { "sizeX": 1, "sizeY": 1, "row": 1, "col": 0, content:'<div class="content">3</div>' },
    { "sizeX": 2, "sizeY": 1, "row": 2, "col": 0, content:'<div class="content">4</div>' },
    { "sizeX": 1, "sizeY": 1, "row": 2, "col": 2, content:'<div class="content">5</div>' },
    { "sizeX": 1, "sizeY": 1, "row": 2, "col": 3, content:'<div class="content">6</div>' }
    ];
}
```

{% endtab %}

## Graphical representation of layout

These cells combinedly forms a grid-structured layout which will be hidden initially. This grid structured layout can be made visible by enabling the `showGridLines` property, which clearly pictures the cells split-up within the layout. These gridlines will be helpful in panels sizing and placement within the layout during initial designing of a dashboard.

In the following sample, the gridlines indicate the cells split-up of the layout and the data containers placed over these cells are known as panels.

{% tab template="dashboard-layout/graphical-representation-of-layout", sourceFiles="app/app.component.ts,app/app.template.html,app/app.module.ts,app/main.ts,app/default-style.css" %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';

@Component({
    selector: 'app-root',
    styleUrls: ['app/default-style.css'],
    templateUrl: 'app/app.template.html',
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
     public cellSpacing: number[] = [10, 10];
    public showGridLines: boolean = true;
    public panels: any = [{ "sizeX": 3, "sizeY": 2, "row": 0, "col": 1, content:'<div class="content">1</div>' },
    { "sizeX": 1, "sizeY": 3, "row": 0, "col": 4, content:'<div class="content">2</div>' },
    { "sizeX": 1, "sizeY": 1, "row": 2, "col": 2, content:'<div class="content">3</div>' },
    { "sizeX": 1, "sizeY": 1, "row": 2, "col": 3, content:'<div class="content">4</div>' }
    ];
}
```

{% endtab %}

## Rendering component in right-to-left direction

It is possible to render the Dashboard Layout in right-to-left direction by setting the [enableRtl](../api/dashboard-layout/#enablertl) API to true.

The following sample demonstrates Dashboard Layout in right-to-left direction.

{% tab template="dashboard-layout/rtl", sourceFiles="app/app.component.ts,app/app.template.html,app/app.module.ts,app/main.ts,app/default-style.css" %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';

@Component({
    selector: 'app-root',
    styleUrls: ['app/default-style.css'],
    templateUrl: 'app/app.template.html',
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    public cellSpacing: number[] = [10, 10];
    public columns: number = 5;
    public enableRtl: boolean = true;
    public panels: any = [
    {'sizeX': 1, 'sizeY': 1, 'row': 0, 'col': 0, header: '<div>Panel 0</div>', content:'<div class="content"></div>'},
    {'sizeX': 3, 'sizeY': 2, 'row': 0, 'col': 1, header: '<div>Panel 1</div>', content:'<div class="content"></div>'},
    {'sizeX': 1, 'sizeY': 3, 'row': 0, 'col': 4, header: '<div>Panel 2</div>', content:'<div class="content"></div>'},
    {'sizeX': 1, 'sizeY': 1, 'row': 1, 'col': 0, header: '<div>Panel 3</div>', content:'<div class="content"></div>'},
    {'sizeX': 2, 'sizeY': 1, 'row': 2, 'col': 0, header: '<div>Panel 4</div>', content:'<div class="content"></div>'},
    {'sizeX': 1, 'sizeY': 1, 'row': 2, 'col': 2, header: '<div>Panel 5</div>', content:'<div class="content"></div>'},
    {'sizeX': 1, 'sizeY': 1, 'row': 2, 'col': 3, header: '<div>Panel 6</div>', content:'<div class="content"></div>'}
    ];

}
```

{% endtab %}