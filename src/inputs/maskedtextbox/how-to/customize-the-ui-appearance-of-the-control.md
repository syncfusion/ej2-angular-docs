# Customize the UI appearance of the control

The appearance of the MaskedTextBox can be changed by adding custom `cssClass` to the component and enabling styles.
Refer to the following example to change the appearance of the MaskedTextBox.

{% tab template="maskedtextbox/custom-css", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // sets mask format to the MaskedTextBox
    template: `
            <div class="col-sm-6">
                <br/><ejs-maskedtextbox #mask="" id="mask1" mask='00000' value= "42648" name="mask_value" cssClass="e-style" placeholder= 'Enter user ID' floatLabelType= 'Always' (focus)= "onfocus($event)"></ejs-maskedtextbox>
            </div>
    `
})

export class AppComponent {
    public onfocus(args): void {
        //sets cursor position at start of MaskedTextBox
        args.selectionEnd= args.selectionStart;
    }
}
```

{% endtab %}