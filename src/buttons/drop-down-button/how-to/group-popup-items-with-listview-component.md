---
title: "Group popup items with ListView component"
component: "DropDownButton"
description: "Angular DropDownButton how to section, hide drop down arrow, group popup items using list view component, dialog open on popup item click."
---

# Group popup items with ListView component

Header in popup items is possible in DropdownButton by templating entire popup with ListView.
Create ListView with id `listview` and provide it as a
[`target`](../../api/drop-down-button#target) for DropDownButton.

In the following example, ListView element is given as `target` to DropDownButton and header
can be achieved by [`groupBy`](../../api/list-view/fieldSettingsModel#groupby) property.

{% tab template="drop-down-button/header", sourceFiles="app/**/*.ts,styles.css", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { ItemModel } from '@syncfusion/ej2-angular-splitbuttons';

@Component({
    selector: 'app-root',
    template: `<!-- To render ListView. -->
               <ejs-listview id='listview' [dataSource]='data' [fields]='field' showCheckBox='true'></ejs-listview>
               <!-- To render DropDownButton. -->
               <button ejs-dropdownbutton target='#listview' iconCss='e-icons e-down' cssClass='e-caret-hide'></button>`
})

export class AppComponent {
   // Initialize action items.
   public items: ItemModel[] = [
        {
            text: 'Cut'
        },
        {
            text: 'Copy'
        },
        {
            text: 'Paste'
        }];
  // Datasource for listview.
  public data: Object = [
    { class: 'data', text: 'Print', id: 'data1', category: 'Customize Quick Access Toolbar' },
    { class: 'data', text: 'Save As', id: 'data2', category: 'Customize Quick Access Toolbar' },
    { class: 'data', text: 'Update Folder', id: 'data3', category: 'Customize Quick Access Toolbar' },
    { class: 'data', text: 'Reply', id: 'data4', category: 'Customize Quick Access Toolbar' }
];

  public field: Object = { text: 'text', groupBy: 'category' };

}
```

{% endtab %}