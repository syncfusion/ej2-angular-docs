---
title: "How To"
component: "DateRangePicker"
description: "Miscellaneous aspects of customizing the date range picker"
---

# Template-driven forms

The form can be build with Angular template syntax easily along with form specific directives.
 This template-driven forms uses the `ng` directives in view to handle the forms controls.

* To enable the template-driven,  import the FormsModule into corresponding app component.

For more details about template-driven Forms refer to:<https://angular.io/guide/forms#template-driven-forms>.

* In angular forms mentioning the name is must to process as form elements.

* Mention the `name` attribute to DateRangePicker element which will be used to identify the
  form element. To register an DateRangePicker element to ngForm,  give the ngModel  to it
  so the FormsModule will  automatically detect the DateRangePicker as a form element.
  After that, the DateRangePicker value will be selected based on the ngModel value.

The following example  demonstrates template driven forms with DateRangePicker component.

{% tab template="daterangepicker/template-driven", isDefaultActive = "true",  sourceFiles="app/**/*.ts,app/**/template.html,styles.css" %}

```typescript
import { Component,ViewChild, ViewEncapsulation, Inject } from '@angular/core';
import { FormGroup, FormBuilder, Validators } from '@angular/forms';
import { DateRangePickerComponent } from '@syncfusion/ej2-angular-calendars';

class User {
    constructor() {
        public range: Date[]
    }
}

@Component({
    selector: 'app-root',
    templateUrl: './app/template.html'
})
export class DefaultDateRangePickerComponent {

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