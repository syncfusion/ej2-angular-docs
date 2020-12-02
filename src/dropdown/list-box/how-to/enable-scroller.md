---
title: "ListBox Scroller"
component: "ListBox"
description: "Angular ListBox component has support to scroll the list items."
---

# Enable Scroller

The ListBox supports scrolling and it can be achieved by restricting the height of the list box using [`height`](../api/list-box/#height) property.

In the following sample, `height` of the list box is restricted to `290px`.

{% tab template="listbox/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-listbox id="listbox" [dataSource]="data" height="290px"></ejs-listbox>`
})

export class AppComponent {
public data: { [key: string]: Object }[] = [
    { text: 'Account Settings', id: 'list-01' },
    { text: 'Address Book', id: 'list-02' },
    { text: 'Delete', id: 'list-03' },
    { text: 'Forward', id: 'list-04' },
    { text: 'Reply', id: 'list-05' },
    { text: 'Reply All', id: 'list-06' },
    { text: 'Save All Attachments', id: 'list-07' },
    { text: 'Save As', id: 'list-08' },
    { text: 'Touch/Mouse Mode', id: 'list-09' },
    { text: 'Undo', id: 'list-10' }
];
}

```

{% endtab %}