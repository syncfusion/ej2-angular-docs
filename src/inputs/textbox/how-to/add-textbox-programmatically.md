---
title: "Add TextBox Programmatically"
component: "Textbox"
description: "Covers customization of the text box component such as a rounded corner, disabled, read-only state, background color, and font color."
---

# Add TextBox Programmatically

* Import the `Input` modules
from `ej2-inputs` library as shown below.

```typescript
import {Input} from '@syncfusion/ej2-inputs';
```

* Pass the `HTML Input` element as parameter to the `createInput` method.

* You can also add the `icons` on the input by passing `buttons` property value with the class
name `e-input-group-icon` as parameter to the `createInput` method.

{% tab template="textbox/getting-started", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { Input } from '@syncfusion/ej2-inputs';

@Component({
    selector: 'app-root',
    template: `<div class="wrap">
                <input id="textbox" type="text" placeholder="Enter Name" />
                <input id="textbox-icon" type="text" />
               </div>`
})

export class AppComponent {
    ngOnInit() {
        let element: HTMLInputElement = document.getElementById('textbox');
        Input.createInput ({
            element: element
        });

        let element1: HTMLInputElement = document.getElementById('textbox-icon');
        Input.createInput ({
            element: element1,
            buttons: ['e-input-group-icon e-input-down'],
            properties: {
                placeholder:'Enter Value'
            }
        });
    }
}

```

{% endtab %}
