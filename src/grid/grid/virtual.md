---
title: "Virtualization"
component: "Grid"
description: "Learn how to improve performance in the Essential JS 2 DataGrid control by using row and column virtualization and grouping with virtualization. Also learn about the limitations of virtualization."
---

# Virtualization

Grid allows you to load large amount of data without performance degradation.

To use virtualization, you need to inject **VirtualScrollService** in Grid.

## Row Virtualization

Row virtualization allows you to load and render rows only in content viewport. It is an alternative way of
paging in which the data will load while scrolling vertically.
To setup the row virtualization, you need to define
[`enableVirtualization`](../api/grid/#enablevirtualization) as true and
content height by [`height`](../api/grid/#height) property.

The number of records displayed in the Grid is determined implicitly by height of content area. Also you have an option to define visible
number of records by
[`pageSettings.pageSize`](../api/grid/pageSettingsModel/#pagesize) property.
The loaded data will be cached and reused when it is needed for next time.

{% tab template="grid/paging1", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { VirtualScrollService } from '@syncfusion/ej2-angular-grids';
import { PageSettingsModel, EditSettingsModel, ToolbarItems } from '@syncfusion/ej2-angular-grids';

const names = ['TOM', 'Hawk', 'Jon', 'Chandler', 'Monica', 'Rachel', 'Phoebe', 'Gunther', 'Ross', 'Geller', 'Joey', 'Bing', 'Tribbiani',
 'Janice', 'Bong', 'Perk', 'Green', 'Ken', 'Adams'];
const hours = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
const designation = ['Manager', 'Engineer 1', 'Engineer 2', 'Developer', 'Tester'];
const status = ['Completed', 'Open', 'In Progress', 'Review', 'Testing']
const data = (count) => {
    const result = [];
    for (let i = 0; i < count; i++) {
        result.push({
          TaskID: i + 1,
          Engineer: names[Math.round(Math.random() * names.length)] || names[0],
          Designation: designation[Math.round(Math.random() * designation.length)] || designation[0],
          Estimation: hours[Math.round(Math.random() * hours.length)] || hours[0],
          Status: status[Math.round(Math.random() * status.length)] || status[0]
        });
    }
    return result;
};

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' height=300 [enableVirtualization]=true [pageSettings]='options' [editSettings]='editSettings' [toolbar]='toolbar'>
                <e-columns>
                    <e-column field='TaskID' headerText='Task ID' textAlign='Right' width=100 isPrimaryKey='true' [validationRules]='rules'></e-column>
                    <e-column field='Engineer' width=100></e-column>
                    <e-column field='Designation' width=100 editType='dropdownedit' [validationRules]='rules'></e-column>
                    <e-column field='Estimation' textAlign='Right' width=100 editType='numericedit' [validationRules]='rules'></e-column>
                    <e-column field='Status' width=100 editType='dropdownedit'></e-column>
                </e-columns>
                </ejs-grid>`,
    providers: [VirtualScrollService]
})
export class AppComponent implements OnInit {

    public data: object[];
    public options: PageSettingsModel;
    public rules: object = { required: true };
    public editSettings: EditSettingsModel;
    public toolbar: ToolbarItems[];
    ngOnInit(): void {
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Normal' };
        this.toolbar = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
        this.data = data(1000);
        this.options = { pageSize: 50 };
    }
}

```

{% endtab %}

## Column Virtualization

Column virtualization allows you to virtualize columns. It will render columns which are in viewport.
You can scroll horizontally to view more columns.

To setup the column virtualization, set the
[`enableVirtualization`](../api/grid/#enablevirtualization) and
[`enableColumnVirtualization`](../api/grid/#enablecolumnvirtualization) properties as `true`.

{% tab template="grid/paging1", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { VirtualScrollService } from '@syncfusion/ej2-angular-grids';
import { PageSettingsModel, EditSettingsModel, ToolbarItems } from '@syncfusion/ej2-angular-grids';

let virtualData = [];
let names: string[] = ['hardire', 'abramjo01', 'aubucch01', 'Hook', 'Rumpelstiltskin', 'Belle', 'Emma', 'Regina', 'Aurora', 'Elsa', 'Anna',
                      'Snow White', 'Prince Charming', 'Cora', 'Zelena', 'August', 'Mulan', 'Graham', 'Discord', 'Will', 'Robin Hood',
                      'Jiminy Cricket', 'Henry', 'Neal', 'Red', 'Aaran', 'Aaren', 'Aarez', 'Aarman', 'Aaron', 'Aaron-James', 'Aarron',
                       'Aaryan', 'Aaryn', 'Aayan', 'Aazaan', 'Abaan', 'Abbas', 'Abdallah', 'Abdalroof', 'Abdihakim', 'Abdirahman',
                     'Abdisalam', 'Abdul', 'Abdul-Aziz', 'Abdulbasir', 'Abdulkadir', 'Abdulkarem', 'Abdulkhader', 'Abdullah',
                     'Abdul-Majeed', 'Abdulmalik', 'Abdul-Rehman', 'Abdur', 'Abdurraheem', 'Abdur-Rahman', 'Abdur-Rehmaan', 'Abel',
                     'Abhinav', 'Abhisumant', 'Abid', 'Abir', 'Abraham', 'Abu', 'Abubakar', 'Ace', 'Adain', 'Adam', 'Adam-James',
                    'Addison', 'Addisson', 'Adegbola', 'Adegbolahan', 'Aden', 'Adenn', 'Adie', 'Adil', 'Aditya', 'Adnan', 'Adrian',
                    'Adrien', 'Aedan', 'Aedin', 'Aedyn', 'Aeron', 'Afonso', 'Ahmad', 'Ahmed', 'Ahmed-Aziz', 'Ahoua', 'Ahtasham',
                     'Aiadan', 'Aidan', 'Aiden', 'Aiden-Jack', 'Aiden-Vee'];

function dataSource(): void {
    for (let i = 0; i < 1000; i++) {
        virtualData.push({
            SNo: i + 1,
            FIELD1: names[Math.floor(Math.random() * names.length)],
            FIELD2: 1967 + (i % 10), FIELD3: Math.floor(Math.random() * 200),
            FIELD4: Math.floor(Math.random() * 100), FIELD5: Math.floor(Math.random() * 2000), FIELD6: Math.floor(Math.random() * 1000),
            FIELD7: Math.floor(Math.random() * 100), FIELD8: Math.floor(Math.random() * 10), FIELD9: Math.floor(Math.random() * 10),
            FIELD10: Math.floor(Math.random() * 100), FIELD11: Math.floor(Math.random() * 100), FIELD12: Math.floor(Math.random() * 1000),
            FIELD13: Math.floor(Math.random() * 10), FIELD14: Math.floor(Math.random() * 10), FIELD15: Math.floor(Math.random() * 1000),
            FIELD16: Math.floor(Math.random() * 200), FIELD17: Math.floor(Math.random() * 300), FIELD18: Math.floor(Math.random() * 400),
            FIELD19: Math.floor(Math.random() * 500), FIELD20: Math.floor(Math.random() * 700), FIELD21: Math.floor(Math.random() * 800),
            FIELD22: Math.floor(Math.random() * 1000), FIELD23: Math.floor(Math.random() * 2000), FIELD24: Math.floor(Math.random() * 150),
            FIELD25: Math.floor(Math.random() * 1000), FIELD26: Math.floor(Math.random() * 100), FIELD27: Math.floor(Math.random() * 400),
            FIELD28: Math.floor(Math.random() * 600), FIELD29: Math.floor(Math.random() * 500), FIELD30: Math.floor(Math.random() * 300),
        });
    }
}
dataSource();
@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' height=300 [enableVirtualization]=true [enableColumnVirtualization]=true
                [pageSettings]='options' [editSettings]='editSettings' [toolbar]='toolbar'>
                <e-columns>
                    <e-column field='SNo' headerText='S.No' width=140 isPrimaryKey='true' [validationRules]='rules'></e-column>
                    <e-column field='FIELD1' headerText='Player Name' width=140 editType='dropdownedit' [validationRules]='rules'></e-column>
                    <e-column field='FIELD2' headerText='Year' width=120 textAlign='Right'></e-column>
                    <e-column field='FIELD3' headerText='Stint' width=120 textAlign='Right'></e-column>
                    <e-column field='FIELD4' headerText='TMID' width=120 textAlign='Right'></e-column>
                    <e-column field='FIELD5' headerText='LGID' width=120 textAlign='Right'></e-column>
                    <e-column field='FIELD6' headerText='GP' width=120 textAlign='Right'></e-column>
                    <e-column field='FIELD7' headerText='GS' width=120 textAlign='Right'></e-column>
                    <e-column field='FIELD8' headerText='Minutes' width=120 textAlign='Right'></e-column>
                    <e-column field='FIELD9' headerText='Points' width=120 textAlign='Right'></e-column>
                    <e-column field='FIELD10' headerText='oRebounds' width=130 textAlign='Right'></e-column>
                    <e-column field='FIELD11' headerText='dRebounds' width=130 textAlign='Right'></e-column>
                    <e-column field='FIELD12' headerText='Rebounds' width=120 textAlign='Right'></e-column>
                    <e-column field='FIELD13' headerText='Assists' width=120 textAlign='Right'></e-column>
                    <e-column field='FIELD14' headerText='Steals' width=120 textAlign='Right'></e-column>
                    <e-column field='FIELD15' headerText='Blocks' width=120 textAlign='Right'></e-column>
                    <e-column field='FIELD16' headerText='Turnovers' width=130 textAlign='Right'></e-column>
                    <e-column field='FIELD17' headerText='PF' width=130 textAlign='Right'></e-column>
                    <e-column field='FIELD18' headerText='fgAttempted' width=150 textAlign='Right'></e-column>
                    <e-column field='FIELD19' headerText='fgMade' width=120 textAlign='Right'></e-column>
                    <e-column field='FIELD20' headerText='ftAttempted' width=150 textAlign='Right'></e-column>
                    <e-column field='FIELD21' headerText='ftMade' width=120 textAlign='Right'></e-column>
                    <e-column field='FIELD22' headerText='ThreeAttempted' width=150 textAlign='Right'></e-column>
                    <e-column field='FIELD23' headerText='ThreeMade' width=130 textAlign='Right'></e-column>
                    <e-column field='FIELD24' headerText='PostGP' width=120 textAlign='Right'></e-column>
                    <e-column field='FIELD25' headerText='PostGS' width=120 textAlign='Right'></e-column>
                    <e-column field='FIELD26' headerText='PostMinutes' width=120 textAlign='Right'></e-column>
                    <e-column field='FIELD27' headerText='PostPoints' width=130 textAlign='Right'></e-column>
                    <e-column field='FIELD28' headerText='PostoRebounds' width=130 textAlign='Right'></e-column>
                    <e-column field='FIELD29' headerText='PostdRebounds' width=130 textAlign='Right'></e-column>
                    <e-column field='FIELD30' headerText='PostRebounds' width=130 textAlign='Right' editType='numericedit' [validationRules]='rules'></e-column>
                </e-columns>
                </ejs-grid>`,
    providers: [VirtualScrollService]
})
export class AppComponent implements OnInit {

    public data: object[];
    public options: PageSettingsModel;
    public editSettings: EditSettingsModel;
    public toolbar: ToolbarItems[];
    public rules: object = { required: true };
    ngOnInit(): void {
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Normal' };
        this.toolbar = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
        this.data = virtualData;
        this.options = { pageSize: 50 };
    }
}

```

{% endtab %}

> Column's [`width`](../api/grid/column/#width) is required for column virtualization.
If column's width is not defined then Grid will consider its value as **200px**.

## Virtualization with Grouping

Both the row and column virtualization can be used along with grouping. At initial rendering, the virtual height of scrollbar will be set based on the total number of records and after grouping, it will be refreshed based on the grouped state(expand/collapse). While collapse the group caption row in current viewport then the next view page grouped records are shown.

> The collapsed/expanded state will persist only for local dataSource while scrolling.

## Limitations for Virtualization

* While using column virtualization, column width should be in pixel. Percentage values are not accepted.
* Due to the element height limitation in browsers, the maximum number of records loaded by the Grid is limited by the browser capability.
* Cell selection will not be persisted in both row and column virtualization.
* Virtual scrolling is not compatible with batch editing, detail template and hierarchy features.
* Group expand and collapse state will not be persisted for remote data.
* Since data is virtualized in grid, the aggregated information and total group items are displayed based on the current view items.
To get these information regardless of the view items, refer to the
[`Group with Page`](./grouping#group-with-paging) topic.
* The page size provided must be two times larger than the number of visible rows in the grid.
If the page size is failed to meet this condition then the size will be determined by grid.
* The height of the grid content is calculated using the row height and total number of records
in the data source and hence features which changes row height such as text wrapping are not supported.
If you want to increase the row height to accommodate the content then you can specify the
 row height as below to ensure all the table rows are in same height.

```css
.e-grid .e-row {
    height: 2em;
}
```

* Programmatic selection using [`selectRows`](../api/grid/#selectrows) method is not supported in virtual scrolling.