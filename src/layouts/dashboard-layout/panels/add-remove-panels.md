---
title: "Adding and removing panels"
component: "DashboardLayout"
description: "This section explains how to add and remove panels dynamically in Essential JS 2 DashboardLayout component"
---
# Adding and removing panels dynamically

In real-time cases, the data being presented within the dashboard should be updated frequently which includes adding or removing the data dynamically within the dashboard. This can be easily achieved by using the `addPanel` and `removePanel` public methods of the component.

## Add or remove panels dynamically

Panels can be added dynamically by using the `addPanel` public method by passing the `panel` property as parameter. Also, they can be removed dynamically by using the `removePanel` public method by passing the `panel id` value as a parameter.

It is also possible to remove all the panels in a Dashboard Layout by calling [removeAll](https://ej2.syncfusion.com/angular/documentation/api/dashboard-layout/#removeall) method.

```js
dashboard.removeAll();

```

The following sample demonstrates how to add and remove the panels dynamically in the dashboard layout component. Here, panels can be added in any desired position of required size by selecting them in the numeric boxes and clicking add button and remove them by selecting the ID of the panel.

{% tab template="dashboard-layout/add-remove-panels", sourceFiles="app/app.component.ts,app/app.template.html,app/app.module.ts,app/main.ts,app/default-style.css" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { ButtonComponent } from '@syncfusion/ej2-angular-buttons';
import { NumericTextBoxComponent } from '@syncfusion/ej2-angular-inputs';
import { DropDownListComponent } from '@syncfusion/ej2-angular-dropdowns';
import { DashboardLayoutComponent } from '@syncfusion/ej2-angular-layouts';

@Component({
    selector: 'app-root',
    styleUrls: ['app/default-style.css'],
    templateUrl: 'app/app.template.html',
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild('defaultLayout') dashboard: DashboardLayoutComponent;
    @ViewChild('sizex') sizeX: NumericTextBoxComponent;
    @ViewChild('sizey') sizeY: NumericTextBoxComponent;
    @ViewChild('row') row: NumericTextBoxComponent;
    @ViewChild('column') column: NumericTextBoxComponent;
    @ViewChild('add') addBtn: ButtonComponent;
    @ViewChild('dropdown') dropDownListObject: DropDownListComponent;

    public data: string[] = ['Panel0', 'Panel1', 'Panel2', 'Panel3', 'Panel4', 'Panel5', 'Panel6'];
    public cellSpacing: number[] = [20, 20];
    public columns: number = 5;
    public count: number = 7;
    public panel: any;
    public panels: any = [{'id':'Panel0', 'sizeX': 1, 'sizeY': 1,'row': 0, 'col': 0, content:'<div class="content">0</div>'},
    {'id':'Panel1', 'sizeX': 3, 'sizeY': 2,'row': 0, 'col': 1, content:'<div class="content">1</div>'},
    {'id':'Panel2', 'sizeX': 1, 'sizeY': 3,'row': 0, 'col': 4, content:'<div class="content">2</div>'},
    {'id':'Panel3', 'sizeX': 1, 'sizeY': 1,'row': 1, 'col': 0, content:'<div class="content">3</div>'},
    {'id':'Panel4', 'sizeX': 2, 'sizeY': 1,'row': 2, 'col': 0, content:'<div class="content">4</div>'},
    {'id':'Panel5', 'sizeX': 1, 'sizeY': 1,'row': 2, 'col': 2, content:'<div class="content">5</div>'},
    {'id':'Panel6','sizeX': 1, 'sizeY': 1,'row': 2, 'col': 3, content:'<div class="content">6</div>'}
    ];
    addClick() {
        this.panel = {
        id: "Panel"+ this.count.toString(),
        sizeX: this.sizeX.value,
        sizeY: this.sizeY.value,
        row: this.row.value,
        col: this.column.value,
        content: "<div class='content'>"+ this.count +"</div>"
        }
        this.dashboard.addPanel(this.panel);
        this.count = this.count + 1;
        (<any>this.dropDownListObject.dataSource).push(this.panel.id);
        this.dropDownListObject.refresh();
    };
    removeClick() {
        this.dashboard.removePanel(<any>this.dropDownListObject.value);
        (<any>this.dropDownListObject.dataSource).splice((<any>this.dropDownListObject.dataSource).indexOf(this.dropDownListObject.value), 1);
        this.dropDownListObject.refresh();
        this.dropDownListObject.value = null;
    };
}
```

{% endtab %}