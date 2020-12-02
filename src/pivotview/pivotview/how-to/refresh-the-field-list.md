# Refresh the field list while change the data source

You can refresh pivot table and field list with new data source dynamically.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { PivotViewComponent, IDataOptions, FieldListService, PivotView } from '@syncfusion/ej2-angular-pivotview';
import { Button } from '@syncfusion/ej2-buttons';

@Component({
  selector: 'app-container',
  providers: [FieldListService],
  // specifies the template string for the pivot table component
  template: `<div class="col-md-8"><ejs-pivotview #pivotview id='PivotView' height='350' [dataSourceSettings]=dataSourceSettings showFieldList="true" width=width></ejs-pivotview></div><div class="col-md-2"><button ej-button id='refresh'>Refresh</button></div>`
})
export class AppComponent implements OnInit {
    public pivotData: IDataSet[];
    public dataSourceSettings: IDataOptions;
    public button: Button;
    public width: string;

    @ViewChild('pivotview',{static: false})
    public pivotGridObj: PivotViewComponent;

    ngOnInit(): void {

        this.pivotData = [
                { 'Sold': 31, 'Amount': 52824, 'Country': 'France', 'Products': 'Mountain Bikes', 'Year': 'FY 2015', 'Quarter': 'Q1' },
                { 'Sold': 51, 'Amount': 86904, 'Country': 'France', 'Products': 'Mountain Bikes', 'Year': 'FY 2015', 'Quarter': 'Q2' },
                { 'Sold': 90, 'Amount': 153360, 'Country': 'France', 'Products': 'Mountain Bikes', 'Year': 'FY 2015', 'Quarter': 'Q3' },
                { 'Sold': 25, 'Amount': 42600, 'Country': 'France', 'Products': 'Mountain Bikes', 'Year': 'FY 2015', 'Quarter': 'Q4' },
                { 'Sold': 27, 'Amount': 46008, 'Country': 'France', 'Products': 'Mountain Bikes', 'Year': 'FY 2016', 'Quarter': 'Q1' }];

        this.dataSourceSettings = {
            dataSource: this.pivotData,
            expandAll: false,
            columns: [{ name: 'Year', caption: 'Production Year' }],
            values: [{ name: 'Sold', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount' }],
            rows: [{ name: 'Country' }],
            formatSettings: [{ name: 'Amount', format: 'C0' }],
            filters: []
        };

        this.width = '100%';

        this.button = new Button({ isPrimary: true });
        this.button.appendTo('#refresh');

        this.button.element.onclick = (): void => {
            this.pivotGridObj.engineModule.fieldList = {};
            this.pivotGridObj.dataSourceSettings.dataSource = [
                  { 'Sold': 31, 'Amount': 52824, 'Country': 'France', 'Year': 'FY 2015' },
                  { 'Sold': 51, 'Amount': 86904, 'Country': 'France', 'Year': 'FY 2015' },
                  { 'Sold': 90, 'Amount': 153360, 'Country': 'France', 'Year': 'FY 2015' },
                  { 'Sold': 25, 'Amount': 42600, 'Country': 'France', 'Year': 'FY 2015' },
                  { 'Sold': 27, 'Amount': 46008, 'Country': 'France', 'Year': 'FY 2016' }];
              };
        };
    }
}
```

{% endtab %}