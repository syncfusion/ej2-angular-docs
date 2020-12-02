# Slider in Angular Reactive Form

Slider validation can be achieved in Angular using [Reactive](https://angular.io/guide/reactive-forms)
forms. Here the sample shown slider validation state based on Angular form
[classes](https://angular.io/guide/forms#track-control-state-and-validity-with-ngmodel).

Follow below steps to validate slider within reactive forms.

* Create simple Angular reactive form. And add simple
[slider](https://ej2.syncfusion.com/angular/documentation/slider/getting-started.html#types)
component within form.

* Create [form group](https://angular.io/guide/reactive-forms#add-a-formgroup) with slider.

```typescript

 sliderForm: FormGroup;
  constructor(fb: FormBuilder) {
    this.value = 30;
    this.sliderForm = fb.group({
      'slider': [0, Validators.min(10)]
    });
  }

  ```

* Show the validation message, based on validation classes which is added to slider. Refer below code snippet.

| **Class if true** | **Class if false** | **state** |
| --- | --- | --- |
| `ng-touched` | `ng-untouched` |The control has been visited. |
| `ng-dirty` | `ng-pristine` |The control's value has changed. |
| `ng-valid` | `ng-invalid` |The control's value is valid. |

```html

<div *ngIf="sliderForm.invalid">
slider has <b><i>invalid </i> </b> value and choose value greater than 10.
</div><br/>
<div *ngIf="sliderForm.valid">
Slider has <b><i>valid </i> </b> value {{value}}.
</div><br/>
<div *ngIf="sliderForm.pristine">
Slider having state <b><i>pristine.</i></b> Slider value not yet changed by user. <br/>
</div>
<div *ngIf="sliderForm.dirty">
Slider having state <b><i>dirty.</i> </b> Slider value changed by user.
</div>
<br/>
<button [disabled]="sliderForm.invalid"  type="submit">submit</button><br/><br/>
<div class="formresult" [hidden]="!validated">
Slider value choosen as: {{value}}
</div>

```

{% tab template="slider/reactiveform", sourceFiles="app/**/*,index.css", isDefaultActive=true %}

```typescript

import { Component, Inject } from '@angular/core';
import { FormGroup, FormBuilder, Validators } from '@angular/forms';

@Component({
    selector: 'my-app',
    templateUrl: 'app/template.html',
    styleUrls:['index.css']
})

export class AppComponent {
  value; slidervalue; validated = false;
  sliderForm: FormGroup;
  constructor(@Inject(FormBuilder) public fb: FormBuilder) {
    this.value = 30;
    this.sliderForm = this.fb.group({
      'slider': [0, Validators.min(10)]
    });
  }
  onSubmit() {
    if (this.sliderForm.valid) {
      this.validated = true;
      console.log('form submitted');
      console.log(this.sliderForm.value.slider);
    }

  }
}

```

{% endtab %}
