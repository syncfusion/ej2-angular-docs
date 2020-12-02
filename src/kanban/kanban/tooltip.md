---
title: "Tooltip of Kanban"
component: "Kanban"
description: "This article demonstrates how to show the tooltip when hovering card elements and also explained how to use template."
---

# Tooltip

The tooltip is used to show the card information when the cursor hover over the card elements using the `enableTooltip` property. Tooltip content is dynamically set based on hovering over the card elements.

> If you wish to show tooltip on Kanban board custom elements, you need to add `e-tooltip-text` class name of a particular element.

## Tooltip template

You can customize the tooltip content with any HTML or CSS element and styling using the `tooltipTemplate` property. In the following demo, the tooltip is customized with HTML elements.

{% tab template="kanban/tooltip-template" sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { CardSettingsModel, SwimlaneSettingsModel } from '@syncfusion/ej2-angular-kanban';
import { kanbanData } from './datasource';

@Component({
  selector: 'app-root',
  template: `<ejs-kanban keyField='Status' [dataSource]='data' [cardSettings]='cardSettings' enableTooltip='true'>
                <e-columns>
                  <e-column headerText='To do' keyField='Open'></e-column>
                  <e-column headerText='In Progress' keyField='InProgress'></e-column>
                  <e-column headerText='Testing' keyField='Testing'></e-column>
                  <e-column headerText='Done' keyField='Close'></e-column>
                </e-columns>
                <ng-template #tooltipTemplate let-data>
                    <div class='e-kanbanTooltipTemp'>
                        <table>
                            <tr>
                                <td class="details">
                                    <table>
                                        <colgroup>
                                            <col style="width:30%">
                                            <col style="width:70%">
                                        </colgroup>
                                        <tbody>
                                            <tr>
                                                <td class="CardHeader">Assignee:</td>
                                                <td>{{data.Assignee}}</td>
                                            </tr>
                                            <tr>
                                                <td class="CardHeader">Type:</td>
                                                <td>{{data.Type}}</td>
                                            </tr>
                                            <tr>
                                                <td class="CardHeader">Estimate:</td>
                                                <td>{{data.Estimate}}</td>
                                            </tr>
                                            <tr>
                                                <td class="CardHeader">Summary:</td>
                                                <td>{{data.Summary}}</td>
                                            </tr>
                                        </tbody>
                                    </table>
                                </td>
                            </tr>
                        </table>
                    </div>
                </ng-template>
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
