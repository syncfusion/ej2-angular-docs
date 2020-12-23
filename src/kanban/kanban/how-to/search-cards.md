---
title: "Searching Cards"
component: "Kanban"
description: "This article demonstrates how to show the cards in Kanban board when you type or search the text in the textbox."
---

# Searching Cards

You can search the cards in Kanban by using the `query` property.

In the following sample, the searching operation starts as soon as you start typing characters in the external text box. It will search the cards based on the `Id` and `Summary` using the `search` query with `contains` operator.

{% tab template="kanban/search-cards" sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { KanbanComponent, CardSettingsModel } from '@syncfusion/ej2-angular-kanban';
import { TextBoxComponent } from '@syncfusion/ej2-angular-inputs';
import { Query } from '@syncfusion/ej2-data';
import { kanbanData } from './datasource';

@Component({
  selector: 'app-root',
  template: `<table>
                <tbody>
                    <td style="width: 200px">
                    <ejs-textbox id="search" #search placeholder="Enter search text" [showClearButton]="true" (keyup)="searchClick($event)"></ejs-textbox>
                    </td>
                    <td>
                    <button ejs-button class="e-btn" id="reset" (click)='reset()'>Reset</button>
                </tbody>
            </table>
            <ejs-kanban #kanban keyField='Status' [dataSource]='data' [cardSettings]='cardSettings'>
                <e-columns>
                  <e-column headerText='To do' keyField='Open'></e-column>
                  <e-column headerText='In Progress' keyField='InProgress'></e-column>
                  <e-column headerText='Testing' keyField='Testing'></e-column>
                  <e-column headerText='Done' keyField='Close'></e-column>
                </e-columns>
            </ejs-kanban>`
})
export class AppComponent {
    @ViewChild('search') textBoxObj: TextBoxComponent;
    @ViewChild('kanban') kanbanObj: KanbanComponent;
    public data: Object[] = kanbanData;
    public cardSettings: CardSettingsModel = {
        contentField: 'Summary',
        headerField: 'Id'
    };
    searchClick(e: KeyboardEvent): void {
        let searchValue: string = (<HTMLInputElement>e.target).value;
        let searchQuery: Query = new Query();
        if (searchValue !== '') {
            searchQuery = new Query().search(searchValue, ['Id', 'Summary'], 'contains', true);
        }
        this.kanbanObj.query = searchQuery;
    }
    reset(): void {
        this.textBoxObj.value = '';
        this.kanbanObj.query = new Query();
    }
}

```

{% endtab %}