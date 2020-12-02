---
title: "Enable or disable items in list box"
component: "ListBox"
description: "Angular ListBox component supports customization of menu items so that the items can be enabled or disabled."
---

# Enable or disable items

To enable or disable items in the list box, [`enableItems`](../api/list-box/#enableitems) method can be used. In the following example, the `Bugatti Veyron Super Sport` and `SSC Ultimate Aero` items are disabled by default and by clicking `Enable Items` buttons, the disabled items will be enabled.

{% tab template="listbox/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { getInstance } from '@syncfusion/ej2-base';
import { ListBox } from '@syncfusion/ej2-dropdowns';

@Component({
    selector: 'app-container',
    template: `<button id="enableitem" (click)="btnclick()" class="e-btn">ENABLE ITEMS</button>
               <ejs-listbox id="listbox" [dataSource]="data" (created)="created()"></ejs-listbox>`
})

export class AppComponent {
public data: { [key: string]: Object }[] = [
    { text: 'Hennessey Venom', id: 'list-01' },
    { text: 'Bugatti Chiron', id: 'list-02' },
    { text: 'Bugatti Veyron Super Sport', id: 'list-03' },
    { text: 'SSC Ultimate Aero', id: 'list-04' },
    { text: 'Koenigsegg CCR', id: 'list-05' },
    { text: 'McLaren F1', id: 'list-06' },
    { text: 'Aston Martin One- 77', id: 'list-07' },
    { text: 'Jaguar XJ220', id: 'list-08' },
    { text: 'McLaren P1', id: 'list-09' },
    { text: 'Ferrari LaFerrari', id: 'list-10' }
];

created():void{
   let listboxobj:ListBox = getInstance(document.getElementById("listbox"), ListBox) as ListBox;
    listboxobj.enableItems(['Bugatti Veyron Super Sport', 'SSC Ultimate Aero'], false);
}

btnclick():void{
  let listboxobj:ListBox = getInstance(document.getElementById("listbox"), ListBox) as ListBox;
  listboxobj.enableItems(['Bugatti Veyron Super Sport', 'SSC Ultimate Aero'], true);
}
}

```

{% endtab %}