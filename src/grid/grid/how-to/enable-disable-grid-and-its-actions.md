---
title: "Enable/Disable Grid and its actions"
component: "Grid"
description: "Learn how to Enable/Disable Grid and its actions."
---

# Enable/Disable Grid and its actions

You can enable/disable the Grid and its actions by applying/removing corresponding CSS styles.

To enable/disable the grid and its actions, follow the given steps:

**Step 1**:

Create CSS class with custom style to override the default style of Grid.

```css
    .disablegrid {
        pointer-events: none;
        opacity: 0.4;
    }
    .wrapper {
        cursor: not-allowed;
    }

```

**Step 2**:

Add/Remove the CSS class to the Grid in the click event handler of Button.

```typescript
    public btnClick():void {
      if (this.Grid.element.classList.contains('disablegrid')) {
          this.Grid.element.classList.remove('disablegrid');
          document.getElementById("GridParent").classList.remove('wrapper');
      }
      else {
          this.Grid.element.classList.add('disablegrid');
          document.getElementById("GridParent").classList.add('wrapper');
      }
    }

```

In the below demo, the button click will enable/disable the Grid and its actions.

{% tab template="grid/edit", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';
import { EditSettingsModel, ToolbarItems, GridComponent } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    template: `<button ejs-button (click)="btnClick()"  cssClass="e-flat">Enable/Disable Grid</button>
               <div id="GridParent">
                    <ejs-grid #Grid [dataSource]='data' [editSettings]='editSettings' [toolbar]='toolbar' height='273px'>
                        <e-columns>
                            <e-column field='OrderID' headerText='Order ID' textAlign='Right' isPrimaryKey='true' width=100></e-column>
                            <e-column field='CustomerID' headerText='Customer ID' width=120></e-column>
                            <e-column field='Freight' headerText='Freight' textAlign= 'Right'
                             editType= 'numericedit' width=120 format= 'C2'></e-column>
                            <e-column field='ShipCountry' headerText='Ship Country' editType= 'dropdownedit' width=150></e-column>
                        </e-columns>
                    </ejs-grid>
               </div>`
})
export class AppComponent implements OnInit {

    public data: object[];
    @ViewChild('Grid') public Grid: GridComponent;
    public editSettings: EditSettingsModel;
    public toolbar: ToolbarItems[];

    ngOnInit(): void {
        this.data = data;
        this.editSettings = { allowAdding: true, allowEditing: true, allowDeleting: true };
        this.toolbar = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
    }
    public btnClick(): void {
        if (this.Grid.element.classList.contains('disablegrid')) {
            this.Grid.element.classList.remove('disablegrid');
            document.getElementById('GridParent').classList.remove('wrapper');
        } else {
            this.Grid.element.classList.add('disablegrid');
            document.getElementById('GridParent').classList.add('wrapper');
        }
    }
}

```

{% endtab %}
