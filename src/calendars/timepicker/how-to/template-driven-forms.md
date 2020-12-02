---
title: "How To"
component: "TimePicker"
description: "Miscellaneous aspects of customizing the time picker"
---

# Template-driven forms

The form can be build with Angular template syntax easily along with form specific directives.
 This template-driven forms uses the `ng` directives in view to handle the forms controls.

* To enable the template-driven,  import the FormsModule into corresponding app component.

For more details about template-driven Forms refer to:<https://angular.io/guide/forms#template-driven-forms>.

* In angular forms mentioning the name is must to process as form elements.

* Mention the `name` attribute to TimePicker element which will be used to identify the
  form element. To register an TimePicker element to ngForm,  give the ngModel  to it
  so the FormsModule will  automatically detect the TimePicker as a form element.
  After that, the TimePicker value will be selected based on the ngModel value.

The following example  demonstrates template driven forms with TimePicker component.

{% tab template="timepicker/template-driven", isDefaultActive = "true",  sourceFiles="app/**/*.ts,app/**/template.html,styles.css" %}

```typescript
import { Component,ViewChild, ViewEncapsulation, Inject } from '@angular/core';
import { FormGroup, FormBuilder, Validators } from '@angular/forms';
import { TimePickerComponent } from '@syncfusion/ej2-angular-calendars';

class User {
    constructor() {
        public time: Date
    }
}

@Component({
    selector: 'app-root',
    templateUrl: './app/template.html'
})
export class DefaultTimePickerComponent {

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