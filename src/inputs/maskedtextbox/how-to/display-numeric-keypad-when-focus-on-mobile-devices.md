# Display numeric keypad when focus on mobile devices

By default, on focusing the MaskedTextBox, alphanumeric keypad will be displayed on
mobile devices. Sometimes only numeric keypad for number
values is needed, and this can be achieved by setting "type" property to `tel`.
Refer to the following example to enable numeric keypad in MaskedTextBox.

{% tab template="maskedtextbox/cursor-position-any", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // sets mask format to the MaskedTextBox
    template: `
            <div class="col-sm-6">
                <br/><ejs-maskedtextbox #mask="" mask='999-99999' value= "342-45432" name="mask_value" type="tel"></ejs-maskedtextbox>
            </div>
    `
})

export class AppComponent {
}
```

{% endtab %}