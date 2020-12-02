# Customize the step value and hide spin buttons

The spin buttons allow you to increase or decrease the value with the predefined [`step`](../../api/numerictextbox#step)
value. The visibility of spin buttons can be set using the[`showSpinButton`](../../api/numerictextbox#showSpinButton) property.

{% tab template="numerictextbox/getting-started", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the NumericTextBox component
    // sets the step value as '2' to increase/decrease the value by '2'
    // sets the showSpinButton value as `false` to hide the spin buttons
    template: `
            <ejs-numerictextbox step='2' [showSpinButton]='false' min='10' max='100' value='16'></ejs-numerictextbox>
            `
})
export class AppComponent {
    constructor() {
    }
}
```

{% endtab %}