# Slider validation using Template-driven Forms

Slider can be validated in Angular using [Template-driven](https://angular.io/guide/form-validation#template-driven-validation)
forms.

* The following [CSS classes](https://angular.io/guide/forms#track-control-state-and-validity-with-ngmodel) will be added on Slider component based on the action done by user.

| **Class if true** | **Class if false** | **state** |
| --- | --- | --- |
| `ng-touched` | `ng-untouched` |The control has been visited. |
| `ng-dirty` | `ng-pristine` |The control's value has changed. |
| `ng-valid` | `ng-invalid` |The control's value is valid. |

{% tab template="slider/templateform", sourceFiles="app/**/*,index.css", isDefaultActive=true %}

```typescript

import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { SliderModule } from '@syncfusion/ej2-angular-inputs';
import {NgForm} from '@angular/forms';

@Component({
    selector: 'my-app',
    templateUrl: 'app/template.html',
    styleUrls:['index.css'],
    encapsulation: ViewEncapsulation.None
})

export class AppComponent {
   value; validated;
  @ViewChild('sliderForm') form: NgForm;
     onSubmit() {
       this.validated = true;
       console.log(this.form.valid)
  }

  ngOnInit() {
   this.value =70;
 }
}

```

{% endtab %}
