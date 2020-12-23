---
title: "Dynamically change Kanban columns"
component: "Kanban"
description: "This article demonstrates how to dynamically change the particular column or complete column in the Kanban board."
---

# Change Kanban columns dynamically

You can dynamically change the Kanban columns by using the [`columns`](../../api/kanban#columns) property.

In the below sample, you can dynamically change the [`allowToggle`](../../api/kanban/columnsModel/#allowtoggle) property at the particular column when you click on the button. You can also change the initially created columns to the new Kanban columns by using the [`columns`](../../api/kanban#columns) property when you click on the button.

{% tab template="kanban/dynamic-columns" sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { KanbanComponent, CardSettingsModel } from '@syncfusion/ej2-angular-kanban';
import { kanbanData } from './datasource';

@Component({
  selector: 'app-root',
  template: `<button ejs-button class="e-btn" id="particularColumn" (click)='toggle()'>Enable Allow Toggle</button>
            <button ejs-button class="e-btn" id="column" (click)='change()'>Change Columns</button>
            <ejs-kanban #kanbanObj keyField='Status' [dataSource]='data' [cardSettings]='cardSettings'>
                <e-columns>
                  <e-column headerText='To do' keyField='Open'></e-column>
                  <e-column headerText='In Progress' keyField='InProgress'></e-column>
                  <e-column headerText='Testing' keyField='Testing'></e-column>
                  <e-column headerText='Done' keyField='Close'></e-column>
                </e-columns>
            </ejs-kanban>`
})
export class AppComponent {
    @ViewChild("kanbanObj") kanbanObj: KanbanComponent;
    public data: Object[] = kanbanData;
    public cardSettings: CardSettingsModel = {
        contentField: 'Summary',
        headerField: 'Id'
    };
    public toggle = (): void => {
        this.kanbanObj.columns[1].allowToggle= true;
    }
    public change = (): void => {
        this.kanbanObj.columns = [
            { headerText: 'To Do', keyField: 'Open' },
            { headerText: 'Done', keyField: 'Close' }
        ]
    }
}

```

{% endtab %}