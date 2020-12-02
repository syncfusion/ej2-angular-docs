---
title: "Form submit"
component: "ButtonGroup"
description: "ButtonGroup how to section, create ButtonGroup using util function, icons, form submit, show selected state on initial render."
---

# Form submit

The name attribute of the input element  is used to group radio/checkbox type ButtonGroup. When the radio/checkbox type are grouped
in form, the checked items value attribute will be posted to server on form submit that can be retrieved through the name. The disabled
radio/checkbox type value will not be sent to the server on form submit.

In the following code snippet, the radio type ButtonGroup is explained with male value as checked.
Now, the value that is in checked state will be sent on form submit.

{% tab template="button-group/default", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<!-- To render ButtonGroup. -->
              <form>
                <div class='e-btn-group'>
                    <input type="radio" id="male" name="gender" value="male" checked/>
                    <label class="e-btn" for="male">Male</label>
                    <input type="radio" id="female" name="gender" value="female"/>
                    <label class="e-btn" for="female">Female</label>
                    <input type="radio" id="transgender" name="gender" value="transgender"/>
                    <label class="e-btn" for="transgender">Transgender</label>
                </div>
                <button class='e-btn e-primary'>Submit</button>
            </form>`
})

export class AppComponent {
}
```

{% endtab %}