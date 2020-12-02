# Add label template with drill down

Yon can add a label template as <div> element to the tree map control when using the label template. To add a label template to the tree map control, you have to hide another labels by setting the `showLabels` property to false in `leafItemSettings` to show only the label template.

To add label template to tree map drilldown, follow the given steps:

**Step 1**:

<!-- markdownlint-disable MD010 -->
Create a tree map control and enable the drill-down option.

```typescript
import { Component, ViewEncapsulation } from '@angular/core';
import { TreeMap, IDrillStartEventArgs } from '@syncfusion/ej2-angular-treemap';
import { CarSales } from './datasource';

/**
 * Default sample
 */
@Component({
  selector: 'app-container',
  template:'<ejs-treemap id="container" #treemap style="display:block;" [dataSource]="dataSource" [weightValuePath]="weightValuePath"enableDrillDown="true" [palette]="palette"><e-levels><e-level groupPath="Continent" [border]="border"></e-level><e-level groupPath="Company" [border]="border"> </e-level></e-levels></ejs-treemap>',
  encapsulation: ViewEncapsulation.None
})
export class TreemapDrillDownComponent {
  public weightValuePath: string = "Sales";
  public palette: string[] = ['white'];
  public dataSource: object[] = CarSales;
  public border: Object = { width: 0.5, color: 'black' }
};
```

**Step 2**:

Add the label template in the `leafItemSettings` options, and then set the `showLabels` property to false to hide another labels and show only label template.

{% tab template= "treemap/how-to/label-template", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';
import { TreeMap, IDrillStartEventArgs } from '@syncfusion/ej2-angular-treemap';
import { CarSales } from './datasource.ts';

@Component({
  selector: 'app-container',
  template:'<ejs-treemap id="container" #treemap style="display:block;" [dataSource]="dataSource" [weightValuePath]="weightValuePath"[leafItemSettings]="leafItemSettings" enableDrillDown="true" (drillStart)="drillStart($event)"[palette]="palette"><e-levels><e-level groupPath="Continent" [border]="border"> </e-level>	<e-level groupPath="Company" [border]="border"></e-level></e-levels></ejs-treemap>',
  encapsulation: ViewEncapsulation.None
})
export class AppComponent implements OnInit {
  public drillStart = (args: IDrillStartEventArgs) => {
    let labelElementGroup: HTMLElement = document.getElementById('container_Label_Template_Group');
    labelElementGroup.remove();
  }
  public weightValuePath: string = "Sales";
  public palette: string[] = ['white'];
  public dataSource: object[] = CarSales;
  public leafItemSettings: object = {
    showLabels: false,
    labelTemplate: '#template',
    templatePosition: 'Center'
  };
  public border: Object = { width: 0.5, color: 'black' }
};
```

{% endtab %}