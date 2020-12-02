# Configure data grid options on editing mode

You can access the data grid options such as sort, group, filter on editing mode using the `beginDrillThrough` event in the pivot table. The event occurs in every value cell on double click and provides the data grid information before display the drill through grid pop-up.

> Grid features are segregated into individual feature-wise modules. For example, to use sorting feature, you should inject `Sort` using the `Grid.Inject(Sort)` section.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component } from '@angular/core';
import { IDataOptions, PivotView, CellEditSettings, BeginDrillThroughEventArgs } from '@syncfusion/ej2-angular-pivotview';
import { Grid, Sort, Filter, Group } from '@syncfusion/ej2-grids';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',  
  template: `<ejs-pivotview #pivotview id='PivotView' height='350' [dataSourceSettings]=dataSourceSettings [editSettings]=editSettings width=width (beginDrillThrough)='beginDrillThrough($event)'></ejs-pivotview>`
})

export class AppComponent {

    public width: string;
    public editSettings: CellEditSettings
    public dataSourceSettings: IDataOptions;

    ngOnInit(): void {

        this.width = "100%";
        this.dataSourceSettings = {
            dataSource: Pivot_Data,
            expandAll: false,
            enableSorting: true,
            drilledMembers: [{ name: 'Country', items: ['France'] }],
            columns: [{ name: 'Year', caption: 'Production Year' }, { name: 'Quarter' }],
            values: [{ name: 'Sold', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount' }],
            rows: [{ name: 'Country' }, { name: 'Products' }],
            formatSettings: [{ name: 'Amount', format: 'C0' }],
            filters: []
        };
        this.editSettings= { allowAdding: true, allowDeleting: true, allowEditing: true, mode: 'Normal' }
    },

    beginDrillThrough(args: BeginDrillThroughEventArgs) {
        if (args.gridObj) {
            Grid.Inject(Sort, Filter, Group);
            let gridObj: Grid = args.gridObj;
            gridObj.allowGrouping = true;
            gridObj.allowSorting = true;
            gridObj.allowFiltering = true;
            gridObj.filterSettings = { type: 'CheckBox' };
        }
    },
 }

```

{% endtab %}
