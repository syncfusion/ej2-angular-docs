---
title: "Kanban State Persistence"
component: "Kanban"
description: "This section explains how to persist the column and swimlane expand/collapse state in the browser’s local storage."
---

# State Persistence

State persistence refers to the Kanban state maintained in the browser's [`localStorage`](https://www.w3schools.com/html/html5_webstorage.asp#) even if the browser is refreshed or if you move to the next page within the browser.

State persistence stores Kanban datasource, column and swimlane expand/collapse state in the local storage when the [`enablePersistence`](../api/kanban/#enablepersistence) is defined as true.

{% tab template="kanban/persistence" sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { CardSettingsModel, SwimlaneSettingsModel } from '@syncfusion/ej2-angular-kanban';
import { kanbanData } from './datasource';

@Component({
  selector: 'app-root',
  template: `<ejs-kanban keyField='Status' [dataSource]='data' [cardSettings]='cardSettings'  [swimlaneSettings]='swimlaneSettings' enablePersistence='true'>
                <e-columns>
                  <e-column headerText='To do' keyField='Open' allowToggle='true'></e-column>
                  <e-column headerText='In Progress' keyField='InProgress' allowToggle='true'></e-column>
                  <e-column headerText='Testing' keyField='Testing' allowToggle='true'></e-column>
                  <e-column headerText='Done' keyField='Close' allowToggle='true'></e-column>
                </e-columns>
            </ejs-kanban>`
})
export class AppComponent {
    public data: Object[] = kanbanData;
    public cardSettings: CardSettingsModel = {
        contentField: 'Summary',
        headerField: 'Id'
    };
    public swimlaneSettings: SwimlaneSettingsModel = { keyField: 'Assignee' };
}

```

{% endtab %}
