---
title: "Group items in Popup"
component: "SplitButton"
description: "Angular SplitButton how to section, group popup items using list view component, dialog open on popup item click."
---

# Group items in Popup

Grouped items are possible in SplitButton by templating entire popup with ListView. Check ListView [`grouping`](../../listview/grouping#grouping) and create such items. Create ListView with id `listview` and provide element of the ListView as target of SplitButton to render it in popup area.

In this following example, ListView is created and its element is set as [`target`](../../api/split-button#target) for SplitButton.

{% tab template="split-button/listview", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<!-- To render ListView. -->
               <ejs-listview id='listview' [dataSource]='listItems' [fields]='field' sortOrder='Descending'></ejs-listview>
               <!-- To render splitbutton. -->
               <ejs-splitbutton content="ClipBoard" target='#listview'></ejs-splitbutton>`
})

export class AppComponent {
    // Datasource for listview.
   public listItems: { [key: string]: Object }[] = [
        {
            'text': 'Cut',
            'category': 'Basic'
        },
        {
            'text': 'Copy',
            'category': 'Basic'
        },
        {
            'text': 'Paste',
            'category': 'Basic'
        },
        {
            'text': 'Paste as Formula',
            'category': 'Advanced'
        },
        {
            'text': 'Paste as Hyperlink',
            'category': 'Advanced'
        },
    ];

    public field: Object = { groupBy: 'category' };
}
```

{% endtab %}