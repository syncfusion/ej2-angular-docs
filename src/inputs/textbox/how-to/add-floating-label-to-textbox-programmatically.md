---
title: "Add Floating Label to TextBox Programmatically"
component: "Textbox"
description: "Covers customization of the text box component such as a rounded corner, disabled, read-only state, background color, and font color."
---

# Add Floating Label to TextBox Programmatically

The `Floating Label TextBox` floats label above the TextBox after focusing, or entering a value in the TextBox.

Floating label supports the types of actions as given below.

Type     | Description
------------ | -------------
  Auto       | The floating label will float above the input after focusing, or entering a value in the input.
  Always     | The floating label will always float above the input.
  Never      | By default, never float the label in the input when the placeholder is available.

* Import the `Input` modules from `ej2-inputs` library as shown in below.

```typescript
import {Input} from '@syncfusion/ej2-inputs';
```

* Pass the `HTML Input` element and `floatLabelType` property as `Auto` to the `createInput` method.

* Set the `placeholder` value to the input element via `element attribute` or pass the parameter to the `createInput` method.

The `watermark label` will be updated based on the specified `placeholder` value of the `Floating Label TextBox`.

* You can add the `icons` on the input by passing `buttons` property value with the
class name `e-input-group-icon` as parameter to the `createInput` method.

{% tab template="textbox/getting-started", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { Input } from '@syncfusion/ej2-inputs';

@Component({
    selector: 'app-root',
    template: `<div class="wrap">
                <h4> FloatLabelType as Auto </h4>
                <input type="text" id="textbox" required/>
                <h4> FloatLabelType as Always </h4>
                <input type="text" id="textbox-01" required/>
                <h4> FloatLabelType as Never </h4>
                <input type="text" id="textbox-02" required/>
                <h4> Float label input with icons </h4>
                <input id="textbox-icon" type="text" />
              </div>`
})

export class AppComponent {
    ngOnInit() {
        let element: HTMLInputElement = document.getElementById('textbox');
        Input.createInput ({
            element: element,
            floatLabelType: "Auto",
            properties: {
                placeholder:'Enter Name'
            }
        });
        let element1: HTMLInputElement = document.getElementById('textbox-01');
        Input.createInput ({
            element: element1,
            floatLabelType: "Always",
            properties: {
                placeholder:'Enter Name'
            }
        });
        let element2: HTMLInputElement = document.getElementById('textbox-02');
        Input.createInput ({
            element: element2,
            floatLabelType: "Never",
            properties: {
                placeholder:'Enter Name'
            }
        });

        let element3: HTMLInputElement = document.getElementById('textbox-icon');
        Input.createInput ({
            element: element3,
            floatLabelType: "Auto",
            buttons: ['e-input-group-icon e-input-down'],
            properties: {
                placeholder:'Enter Value'
            }
        });
    }
}

```

{% endtab %}
