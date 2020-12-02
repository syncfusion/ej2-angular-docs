# Customize the UI appearance of the control

You can change the appearance of the NumericTextBox by adding custom `cssClass` to the component and enabling styles. Refer to the following example to change the appearance of the NumericTextBox.

{% tab template="numerictextbox/custom-css", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the NumericTextBox component
    // sets the custom css for NumericTextBox
    template: `
            <ejs-numerictextbox  cssClass='e-style'  value='10'  placeholder= 'Enter Value' floatLabelType= 'Always'  ></ejs-numerictextbox>
            `
})
export class AppComponent {
    constructor() {
    }
}
```

{% endtab %}