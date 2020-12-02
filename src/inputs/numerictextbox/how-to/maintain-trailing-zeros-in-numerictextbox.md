# Maintain trailing zeros in NumericTextBox

By default, trailing zeros disappear when the NumericTextBox gets focus. However, you can use the following sample to maintain the trailing zeros while focusing the NumericTextBox.

{% tab template="numerictextbox/trailing-zeros", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript
import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the NumericTextBox component

    template: `
            <ejs-numerictextbox #numeric='' id="numeric"  decimals='2' format='n2' value='10'  placeholder= 'NumericTextBox' floatLabelType= 'Always' (change)="onChange($event)" (created)="onCreate($event)" ></ejs-numerictextbox>
            `
})
export class AppComponent {
    public onChange(args) {
        var numericObj =  numeric.ej2_instances[0];
        numericObj.element.value = numericObj.formattedValue(numericObj.decimals, +numericObj.element.value);
    }
    public onCreate(): void {
        document.getElementById("numeric").addEventListener('focus',function(){
            var numericObj = this.ej2_instances[0];
            numericObj.element.value = numericObj.formattedValue(numericObj.decimals, +numericObj.element.value);
        });
    }
    constructor() {
    }
}

```

{% endtab %}