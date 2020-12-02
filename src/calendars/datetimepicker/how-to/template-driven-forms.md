---
title: "How To"
component: "DateTimePicker"
description: "Miscellaneous aspects of customizing the date time picker"
---

# Template-driven forms

The form can be build with Angular template syntax easily along with form specific directives.
 This template-driven forms uses the `ng` directives in view to handle the forms controls.

* To enable the template-driven,  import the FormsModule into corresponding app component.

For more details about template-driven Forms refer to:<https://angular.io/guide/forms#template-driven-forms>.

* In angular forms mentioning the name is must to process as form elements.

* Mention the `name` attribute to DateTimePicker element which will be used to identify the
  form element. To register an DateTimePicker element to ngForm,  give the ngModel  to it
  so the FormsModule will  automatically detect the DateTimePicker as a form element.
  After that, the DateTimePicker value will be selected based on the ngModel value.

The following example  demonstrates template driven forms with DateTimePicker component.

{% tab template="datetimepicker/template-driven", isDefaultActive = "true",  sourceFiles="app/**/*.ts,app/**/template.html,styles.css" %}

```typescript
import { Component,ViewChild, Inject } from '@angular/core';
import { FormGroup, FormBuilder, Validators } from '@angular/forms';
import { DateTimePickerComponent } from '@syncfusion/ej2-angular-calendars';

class User {
    constructor() {
        public datetime: Date
    }
}

@Component({
    selector: 'app-root',
    templateUrl: './app/template.html'
})
export class DefaultDateTimePickerComponent {
    constructor() {}
    user: User;
    ngOnInit() {
        this.user = new User(null);
    }

    onSubmit(userForm) {
        (userForm.valid) ? alert("submitted"): alert("form is invalid");
    }

}
```

{% endtab %}
