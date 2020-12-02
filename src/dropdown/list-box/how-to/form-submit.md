---
title: "Form submit to the list box"
component: "ListBox"
description: "Angular ListBox component supports form submit to the list box."
---

# Form submit to the list box

In the following code snippet, the value that is in selected state will be sent on form submit.

{% tab template="listbox/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<form><ejs-listbox id="listbox" [dataSource]="data" height="290px"></ejs-listbox>
               <button class="e-btn">Submit</button></form>`
})

export class AppComponent {
public data: { [key: string]: Object }[] = [
    { text: 'Hennessey Venom' },
    { text: 'Bugatti Chiron' },
    { text: 'Bugatti Veyron Super Sport' },
    { text: 'SSC Ultimate Aero' },
    { text: 'Koenigsegg CCR' },
    { text: 'McLaren F1' },
    { text: 'Aston Martin One- 77' },
    { text: 'Jaguar XJ220' },
    { text: 'McLaren P1' },
    { text: 'Ferrari LaFerrari' },
];
}

```

{% endtab %}