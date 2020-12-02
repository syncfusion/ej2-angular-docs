---
title: "Columns in Kanban board"
component: "Kanban"
description: "This section explains how to create a columns in Kanban board with header template, toggle columns and validation."
---

# Columns in Kanban Board

The **Kanban** columns represent the each stage of the process. The column definitions are used as the **dataSource** schema in the Kanban. The Kanban operations such as drag-and-drop, swimlane, and toggle columns are performed based on column definitions.

## Single-key mapping

Kanban columns are categorized by mapping the **key** from the datasource using the `keyField` property. The corresponding **value** in the datasource is mapped inside the columns `keyField`.  Based on this categorization, Kanban columns are split on this board.

> The `keyField` property is mandatory to render the columns in the Kanban board.

{% tab template="kanban/single-key" sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { CardSettingsModel } from '@syncfusion/ej2-angular-kanban';
import { kanbanData } from './datasource';

@Component({
  selector: 'app-root',
  template: `<ejs-kanban keyField='Status' [dataSource]='data' [cardSettings]='cardSettings'>
                <e-columns>
                  <e-column headerText='To do' keyField='Open'></e-column>
                  <e-column headerText='In Progress' keyField='InProgress'></e-column>
                  <e-column headerText='Testing' keyField='Testing'></e-column>
                  <e-column headerText='Done' keyField='Close'></e-column>
                </e-columns>
            </ejs-kanban>`
})
export class AppComponent {
    public data: Object[] = kanbanData;
    public cardSettings: CardSettingsModel = {
        contentField: 'Summary',
        headerField: 'Id'
    };
}

```

{% endtab %}

## Multi-key mapping

Kanban board allows to render a single column by mapping multiple keys using `keyField` property. In below sample, specified the multiple keys(Open, Validate) to a single column.

{% tab template="kanban/multiple-keys" sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { CardSettingsModel } from '@syncfusion/ej2-angular-kanban';
import { kanbanData } from './datasource';

@Component({
  selector: 'app-root',
  template: `<ejs-kanban keyField='Status' [dataSource]='data' [cardSettings]='cardSettings'>
                <e-columns>
                  <e-column headerText='To do' keyField='Open, Validate'></e-column>
                  <e-column headerText='In Progress' keyField='InProgress'></e-column>
                  <e-column headerText='Testing' keyField='Testing'></e-column>
                  <e-column headerText='Done' keyField='Close'></e-column>
                </e-columns>
            </ejs-kanban>`
})
export class AppComponent {
    public data: Object[] = kanbanData;
    public cardSettings: CardSettingsModel = {
        contentField: 'Summary',
        headerField: 'Id'
    };
}

```

{% endtab %}

## Header text

You can provide the column header text of Kanban columns using the `headerText` property. If you have not specified any header text, it will render the header without any text.

## Header template

You can customize the column header with any HTML or CSS element using the `template` property as shown in the following code.

{% tab template="kanban/header-template" sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { CardSettingsModel, ColumnsModel } from '@syncfusion/ej2-angular-kanban';
import { kanbanData } from './datasource';

@Component({
  selector: 'app-root',
  template: `<ejs-kanban keyField='Status' cssClass='kanban-header-template' [dataSource]='data' [cardSettings]='cardSettings'>
                <e-columns>
                    <e-column *ngFor="let column of columns;" headerText={{column.headerText}} keyField='{{column.keyField}}'>
                        <ng-template #template let-data>
                            <div class="header-template-wrap">
                                <div class="header-icon e-icons {{data.keyField}}"></div>
                                <div class="header-text">{{data.headerText}}</div>
                            </div>
                        </ng-template>
                    </e-column>
                </e-columns>
            </ejs-kanban>`
})
export class AppComponent {
    public data: Object[] = kanbanData;
    public cardSettings: CardSettingsModel = {
        headerField: 'Id',
        contentField: 'Summary'
    };
    public columns: ColumnsModel[] = [
        { headerText: 'To Do', keyField: 'Open' },
        { headerText: 'In Progress', keyField: 'InProgress' },
        { headerText: 'In Review', keyField: 'Review' },
        { headerText: 'Done', keyField: 'Close' }
    ];
}

```

{% endtab %}

## Toggle columns

Kanban allows to expand or collapse its columns using `allowToggle` inside the `columns` property. When enable the property, it will render the expand or collapse icon to the column header.

> By default, collapsed column width is set to `50px`.

{% tab template="kanban/toggle" sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { CardSettingsModel } from '@syncfusion/ej2-angular-kanban';
import { kanbanData } from './datasource';

@Component({
  selector: 'app-root',
  template: `<ejs-kanban keyField='Status' [dataSource]='data' [cardSettings]='cardSettings'>
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
}

```

{% endtab %}

### Initially collapsed column

By default, all columns are on expanded state when loading the Kanban board initially. But, you can render the columns with collapsed state using the `isExpanded` property.

>The `isExpanded` property only works when enabling the `allowToggle` property on particular column.

In the following example, the backlog column is collapsed on initialization of Kanban board.

{% tab template="kanban/expanded" sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { CardSettingsModel } from '@syncfusion/ej2-angular-kanban';
import { kanbanData } from './datasource';

@Component({
  selector: 'app-root',
  template: `<ejs-kanban keyField='Status' [dataSource]='data' [cardSettings]='cardSettings'>
                <e-columns>
                  <e-column headerText='To do' keyField='Open' allowToggle='true' [isExpanded]='isExpanded'></e-column>
                  <e-column headerText='In Progress' keyField='InProgress' allowToggle='true'></e-column>
                  <e-column headerText='Testing' keyField='Testing' allowToggle='true' [isExpanded]='isExpanded'></e-column>
                  <e-column headerText='Done' keyField='Close' allowToggle='true'></e-column>
                </e-columns>
            </ejs-kanban>`
})
export class AppComponent {
    public data: Object[] = kanbanData;
    public isExpanded: Boolean = false;
    public cardSettings: CardSettingsModel = {
        contentField: 'Summary',
        headerField: 'Id'
    };
}

```

{% endtab %}

## Stacked headers

Stacked headers are the additional headers to column header that will group the similar columns.

Define the grouping of columns **key** value to the `keyFields` property and provide the custom header text name to grouped columns using the `text` property, which is placed inside the `stackedHeaders` property.

In the following code, the kanban columns 'InProgress, Review' are grouped under 'Development Phase' category.

{% tab template="kanban/stacked-headers" sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { CardSettingsModel } from '@syncfusion/ej2-angular-kanban';
import { kanbanData } from './datasource';

@Component({
  selector: 'app-root',
  template: `<ejs-kanban keyField='Status' [dataSource]='data' [cardSettings]='cardSettings'>
                <e-columns>
                    <e-column headerText='Open' keyField='Open'></e-column>
                    <e-column headerText='In Progress' keyField='InProgress'></e-column>
                    <e-column headerText='Review' keyField='Review'></e-column>
                    <e-column headerText='Completed' keyField='Close'></e-column>
                </e-columns>
                <e-stackedHeaders>
                    <e-stackedHeader text='To Do' keyFields='Open'></e-stackedHeader>
                    <e-stackedHeader text='Development Phase' keyFields='InProgress, Review'></e-stackedHeader>
                    <e-stackedHeader text='Done' keyFields='Close'></e-stackedHeader>
                </e-stackedHeaders>
            </ejs-kanban>`
})
export class AppComponent {
    public data: Object[] = kanbanData;
    public cardSettings: CardSettingsModel = {
        contentField: 'Summary',
        headerField: 'Id'
    };
}

```

{% endtab %}
