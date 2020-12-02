---
title: "Row"
component: "TreeGrid"
description: "Documentation for row customizations in TreeGrid."
---

# Row

The row represents record details fetched from data source.

## Customize rows

You can customize the appearance of a row by using the [`rowDataBound`](../api/treegrid/#rowdatabound) event.
The [`rowDataBound`](../api/treegrid/#rowdatabound) event triggers for every row. In the event handler, you can get the
`RowDataBoundEventArgs` that contains details of the row.

{% tab template="treegrid/row", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';
import {RowDataBoundEventArgs} from '@syncfusion/ej2-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' [treeColumnIndex]='1' height='315' [enableHover]='false' (rowDataBound)='rowBound($event)' childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' width=90></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];

    ngOnInit(): void {
        this.data = sampleData;
    }
 rowBound(args: RowDataBoundEventArgs) {
    if (args.data['duration'] == 0 ) {
        args.row.style.background= '#336c12';
    } else if (args.data['duration'] < 3) {
        args.row.style.background= '#7b2b1d';
    }
}
}

```

{% endtab %}

## Styling alternate rows

 You can change the treegrid's alternative rows' background color by overriding the `.e-altrow` class.

```css
.e-treegrid .e-altrow {
    background-color: #fafafa;
}
```

> The above style customization works only when we elevate the CSS to global scope using the encapsulation: ViewEncapsulation.None
> If you need to apply style for ViewEncapsulation other than None, use ng-deep like shown in the below example code snippet,

```css
::ng-deep .e-treegrid .e-altrow  {
    background-color: #fafafa;
}
```

Please refer to the following example.

{% tab template="treegrid/alt-row", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit, ViewEncapsulation } from '@angular/core';
import { sampleData } from './datasource';

@Component({
    selector: 'app-container',
    encapsulation: ViewEncapsulation.None,
    template: `<ejs-treegrid [dataSource]='data' [treeColumnIndex]='1' height='315' [enableHover]='false' childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' width=90></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];

    ngOnInit(): void {
        this.data = sampleData;
    }
}
```

{% endtab %}

## Row height

You can customize the row height of treegrid rows through the [`rowHeight`](../api/treegrid/#rowheight) property. The `rowHeight` property
is used to change the row height of entire treegrid rows.

In the below example, the `rowHeight` is set as '60px'.

{% tab template="treegrid/row", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' height='315' [treeColumnIndex]='1' rowHeight='60' childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' width=90></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];

    ngOnInit(): void {
        this.data = sampleData;
    }
}

```

{% endtab %}

### Customize row height for particular row

Grid row height for particular row can be customized using the [`rowDataBound`](../api/treegrid/#rowdatabound)
event by setting the `rowHeight` in arguments for each row based on the requirement.

In the below example, the row height for the row with Task ID as '3' is set as '90px' using the `rowDataBound` event.

{% tab template="treegrid/row", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';
import {RowDataBoundEventArgs} from '@syncfusion/ej2-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' height='315' [treeColumnIndex]='1' (rowDataBound)='onRowBound($event)' childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' width=90></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];

    ngOnInit(): void {
        this.data = sampleData;
        interface TasKDetails {
    taskID ?: number;
}
    }
 onRowBound(args: RowDataBoundEventArgs) {
   if((args.data as TasKDetails).taskID === 3){
        args.rowHeight = 90;
    }
}
}

```

{% endtab %}

## Row template

The [`rowTemplate`](../api/treegrid/#rowtemplate) has an option to customise the look and behavior of the treegrid rows. The [`rowTemplate`](../api/treegrid/#rowtemplate) property accepts either the template string or HTML element ID.

{% tab template="treegrid/rowtemplate", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit, ViewChild, ViewEncapsulation } from '@angular/core';
import { textdata } from './datasource';
import { TreeGridComponent } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid #treegrid [dataSource]='data' height=291 width='auto' childMapping= 'Children' >
                <e-columns>
                        <e-column field = 'EmpID' headerText = 'Employee ID' width = '180'></e-column>
                        <e-column field = 'Name' headerText = 'Employee Name' width = '150'></e-column>
                        <e-column field = 'Address' headerText = 'Employee Details' width = '350'></e-column>
                </e-columns>
        <ng-template #rowTemplate let-data>
                <tr>
                        <td class="border" style='padding-left:18px;'>
                            <div>{{data.EmpID}}</div>
                        </td>
                        <td class="border" style='padding: 10px 0px 0px 20px;'>
                            <div style="font-size:14px;">
                              {{data.Name}}
                                <p style="font-size:9px;">{{data.Designation}}</p>
                            </div>
                        </td>
                        <td class="border">
                            <div>
                                <div style="position:relative;display:inline-block;">
                                    <img src="{{data.FullName}}.png" alt="{{data.FullName}}" />
                                </div>
                                <div style="display:inline-block;">
                                    <div style="padding:5px;">{{data.Address}}</div>
                                    <div style="padding:5px;">{{data.Country}}</div>
                                    <div style="padding:5px;font-size:12px;">{{data.Contact}}</div>
                                </div>
                            </div>
                        </td>
                </tr>
        </ng-template>
</ejs-treegrid>`,
styleUrls: ['./app/app.style.css']
})
export class AppComponent implements OnInit {

    public data: Object[];

    @ViewChild('treegrid')
    public treegrid: TreeGridComponent;

    ngOnInit(): void {
        this.data = textdata;
    }
}

```

{% endtab %}

The [`rowTemplate`](../api/treegrid/#rowtemplate) property accepts only the TR element.

### Row template with formatting

If the [`rowTemplate`](../api/treegrid/#rowtemplate) is used, the value cannot be  formatted  inside the template using the [`columns.format`](../api/treegrid/column/#format) property. In that case, a function should be defined globally to format the value and invoke it inside the template.

{% tab template="treegrid/rowtemplateformat", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit, ViewChild, ViewEncapsulation } from '@angular/core';
import { textdata } from './datasource';
import { TreeGridComponent } from '@syncfusion/ej2-angular-treegrid';
import { Internationalization } from '@syncfusion/ej2-base';

let instance: Internationalization = new Internationalization();

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid #treegrid [dataSource]='data' height=291 width='auto' childMapping= 'Children' >
                <e-columns>
                        <e-column field = 'EmpID' headerText = 'Employee ID' width = '180'></e-column>
                        <e-column field = 'Address' headerText = 'Employee Details' width = '350'></e-column>
                        <e-column field = 'DOB' headerText = 'DOB' width = '150'></e-column>
                </e-columns>
        <ng-template #rowTemplate let-data>
                <tr>
                        <td class="border" style='padding-left:18px;'>
                            <div>{{data.EmpID}}</div>
                        </td>
                        <td class="border">
                            <div>
                                <div style="position:relative;display:inline-block;">
                                    <img src="{{data.FullName}}.png" alt="{{data.FullName}}" />
                                </div>
                                <div style="display:inline-block;">
                                    <div style="padding:5px;">{{data.Address}}</div>
                                    <div style="padding:5px;">{{data.Country}}</div>
                                    <div style="padding:5px;font-size:12px;">{{data.Contact}}</div>
                                </div>
                            </div>
                        </td>
                        <td class="border" style='padding-left: 20px;'>
                            <div>{{format(data.DOB)}}</div>
                        </td>
                </tr>
        </ng-template>
</ejs-treegrid>`,
styleUrls: ['./app/app.style.css']
})
export class AppComponent implements OnInit {

    public data: Object[];

    @ViewChild('treegrid')
    public treegrid: TreeGridComponent;

    ngOnInit(): void {
        this.data = textdata;
    }

    public format(value: Date): string {
        return instance.formatDate(value, { skeleton: 'yMd', type: 'date' });
    }
}
export interface DateFormat extends Window {
    format?: Function;
}

```

{% endtab %}

### Limitations

Row template feature is not compatible with all the features which are available in treegrid and it has limited features support. Here we have listed out the features which are compatible with row template feature.

* Filtering
* Paging
* Sorting
* Scrolling
* Searching
* Rtl
* Context Menu
* State Persistence

## Detail template

The detail template provides additional information about a particular row. By expanding the parent row the child rows are expanded along with their detail template. The [`detailTemplate`](../api/treegrid/#detailtemplate) property accepts either the template string or HTML element ID.

{% tab template="treegrid/detailtemplate", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit, ViewEncapsulation, ViewChild } from '@angular/core';
import { TreeGridComponent, DetailRowService } from '@syncfusion/ej2-angular-treegrid';
import { textdata } from './datasource';
import { Internationalization } from '@syncfusion/ej2-base';

let instance: Internationalization = new Internationalization();

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid #treegrid [dataSource]='data' height=317 width='auto' childMapping= 'Children' >
            <e-columns>
                <e-column field='Name' headerText='First Name' width='160'></e-column>
                <e-column field='DOB' headerText = 'DOB' width='105' type='date' format='yMd'></e-column>
                <e-column field='Designation' headerText = 'Designation' width='180'></e-column>
                <e-column field='Country' headerText = 'Country' width='148'></e-column>
            </e-columns>
        <ng-template #detailTemplate let-data>
            <div>
                <div style="position: relative; display: inline-block; float: left; font-weight: bold; width: 10%;padding:5px 4px 2px 27px;;">
                   <img src="{{data.FullName}}.png" alt="{{data.FullName}}"/>
               </div>
               <div style="padding-left: 10px; display: inline-block; width: 66%; text-wrap: normal;font-size:13px;font-family:'Segoe UI';">
                   <div class="e-description" style="word-wrap: break-word;">
                       <b>{{data.Name}}</b> was born on {{format(data.DOB)}}. Now lives at {{data.Address}}, {{data.Country}}. {{data.Name}} holds a position of <b>{{data.Designation}}</b> in our WA department, (Seattle USA).
                   </div>
                   <div class="e-description" style="word-wrap: break-word;margin-top:5px;">
                       <b style="margin-right:10px;">Contact:</b>{{data.Contact}}
                   </div>
               </div>
           </div>
        </ng-template>
</ejs-treegrid>`,
providers: [DetailRowService]
})
export class AppComponent implements OnInit {

    public data: Object[];

    @ViewChild('treegrid')
    public treegrid: TreeGridComponent;

    ngOnInit(): void {
        this.data = textdata;
    }

    public format(value: Date): string {
        return instance.formatDate(value, { skeleton: 'yMd', type: 'date' });
    }
}
export interface DateFormat extends Window {
    format?: Function;
}

```

{% endtab %}

## Drag and drop

The TreeGrid rows can be reordered, dropped to another TreeGrid or custom control by enabling the [`allowRowDragAndDrop`](../api/treegrid/#allowrowdraganddrop) to true.

To use row drag and drop, inject the `RowDDService` module in the TreeGrid.

### Drag and drop within TreeGrid

The TreeGrid row drag and drop allows you to drag and drop TreeGrid rows on the same TreeGrid using drag icon. To enable row drag and drop, set the [`allowRowDragAndDrop`](../api/treegrid/#allowrowdraganddrop) to true. It provides the way to drop the row above, below or child to the target row with respective to the target row position.

{% tab template="treegrid/draganddrop", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';

@Component({
    selector: 'app-container',
    template: `
        <ejs-treegrid id='TreeGrid' [dataSource]='data' height='315' [allowRowDragAndDrop]='true' [treeColumnIndex]='1' [rowDropSettings]='rowDrop'
         [selectionSettings]='selectionSettings'
         childMapping='subtasks' >
            <e-columns>
                        <e-column field='taskID' headerText='Task ID' [isPrimaryKey]='true' textAlign='Right' width=90></e-column>
                        <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                        <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' width=90></e-column>
                        <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
            </e-columns>
        </ejs-treegrid>
    `
})
export class AppComponent implements OnInit {
    public data: Object[];
    public rowDrop: Object;
    public selectionSettings: Object;
    ngOnInit(): void {
        this.data = sampleData;
    }
}

```

{% endtab %}

> * Selection feature must be enabled for row drag and drop.
> * For multiple row selection, the [`type`](../api/treegrid/selectionSettings/#type) property must be set to `multiple`.

### Drag and drop to another TreeGrid

To drag and drop between two TreeGrid, enable the [`allowRowDragAndDrop`](../api/treegrid/#allowrowdraganddrop) property and specify the target TreeGrid ID in [`targetID`](../api/treegrid/rowDropSettings/#targetid) property of rowDropSettings.

{% tab template="treegrid/draganddrop", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<div>
    <div style="float:left;width:49%">
        <ejs-treegrid id='TreeGrid' [dataSource]='data' [allowRowDragAndDrop]='true' height='315' [treeColumnIndex]='1' [rowDropSettings]='rowDrop'
         [selectionSettings]='selectionSettings'
         childMapping='subtasks' >
            <e-columns>
                        <e-column field='taskID' headerText='Task ID' [isPrimaryKey]='true' textAlign='Right' width=90></e-column>
                        <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                        <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' width=90></e-column>
                        <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
            </e-columns>
        </ejs-treegrid>
    </div>
    <div style="float:left;width:49%">
        <ejs-treegrid id='destTree' height='315' [allowRowDragAndDrop]='true' [treeColumnIndex]='1' [rowDropSettings]='rowDrops' childMapping='subtasks'
        [selectionSettings]='selectionSettings'
        >
            <e-columns>
                    <e-column field='taskID' headerText='Task ID' [isPrimaryKey]='true' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' width=90></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
            </e-columns>
        </ejs-treegrid>
    </div>
    </div>
    `
})
export class AppComponent implements OnInit {
    public data: Object[];
    public rowDrop: Object;
    public rowDrops: Object;
    public selectionSettings: Object;
    ngOnInit(): void {
        this.data = sampleData;
        this.selectionSettings = { type: 'Multiple' };
        this.rowDrop = { targetID: 'destTree' };
        this.rowDrops = { targetID: 'TreeGrid' };
    }
}

```

{% endtab %}

### Drag and drop events

The following events are triggered while drag and drop the treegrid rows.

[`rowDragStartHelper`](../api/treegrid/#rowdragstarthelper) - Triggers when click the drag icon or treegrid row and this event is used to customize the drag element based on user criteria.<br/>
[`rowDragStart`](../api/treegrid/#rowdragstart) -Triggers when starts to drag the treegrid row. <br/>
[`rowDrag`](../api/treegrid/#rowdrag) - Triggers while dragging the treegrid row. <br/>
[`rowDrop`](../api/treegrid/#rowdrop) - Triggers when a drag element is dropped on the target element. <br/>