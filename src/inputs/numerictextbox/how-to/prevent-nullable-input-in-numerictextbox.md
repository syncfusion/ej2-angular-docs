# Prevent nullable input in NumericTextBox

By default, the value of the NumericTextBox sets to null. In some applications, the value of the NumericTextBox should not be null at any instance. In such cases, following sample can be used to prevent nullable input in NumericTextBox.

{% tab template="numerictextbox/nullable-input", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { NumericTextBoxComponent } from '@syncfusion/ej2-angular-inputs';

@Component({
    selector: 'app-root',
    // specifies the template string for the NumericTextBox component
    template: `
            <ejs-numerictextbox #numeric=""  id="numeric" placeholder= 'NumericTextBox' floatLabelType= 'Always' (created)="onCreate($event)"  (blur)="onBlur($event)" ></ejs-numerictextbox>
            `
})
export class AppComponent {
   @ViewChild('numeric') numeric: NumericTextBoxComponent;
   public onCreate() {
            if (this.numeric.value == null) {
              this.numeric.value = 0;
           }
   }
   public onBlur(args) {
     if(args.value == null) {
      this.numeric.value = 0;
     }
   }
   constructor() {
   }
}

```

{% endtab %}