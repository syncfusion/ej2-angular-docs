# Form slider with FormValidator

We can validate the Slider component using our `FormValidator`. The following steps walk-through
for slider validation.

* Render Slider component inside form.

* Bind [changed](https://ej2.syncfusion.com/angular/documentation/slider/api-sliderComponent.html#changed)
event in the Slider component to validate the slider value when the value changes.

* Initialize and render FormValidator for the form using form ID.

* Set required property in the FormValidator `rules` collection.
Here, we set the
[min](https://ej2.syncfusion.com/angular/documentation/slider/api-sliderComponent.html#min)
property of Slider which sets the minimum value in Slider component and it has hidden
input since enable `validateHidden` property as true.

```typescript

//slider element
<ejs-slider id='default'></ejs-slider>
// sets required property in the FormValidator rules collection
export class AppComponent {
    @ViewChild('formId') element:any;
    public formObject: FormValidator;
    ngAfterViewInit() {
      let options: FormValidatorModel = {
        rules: {
          'default': {
            validateHidden: true,
            min: [6, "You must select value greater than 5"]
          }
        }
      };
      this.formObject = new FormValidator(this.element.nativeElement, options);
    }
}

```

> Form validation done by either ID or name value of Slider component. In above used ID of the
slider for validate it.

Using Slider name: Render Slider with name attribute. In the below code snippet we have used name
attribute value of ‘slider’ for form validation.

```typescript

//slider element with name attribute
<ejs-slider id='default' name='slider'></ejs-slider>
// sets required property in the FormValidator rules collection
export class AppComponent {
    @ViewChild('formId') element:any;
    public formObject: FormValidator;
    ngAfterViewInit() {
      let options: FormValidatorModel = {
        rules: {
          'slider': {
            validateHidden: true,
            min: [30, "You must select value greater than 30"]
          }
        }
      };
      this.formObject = new FormValidator(this.element.nativeElement, options);
    }
}

```

* Validate the form using `validate` method and it validates the Slider value with the defined
rules collection and returns the result.
If user selects the value less than the minimum value, form will not submit.

```typescript

this.formObject.validate();

```

* Slider validation can be done during value changes in slider. Refer to the below code snippet.

```typescript

  public onChanged(): void {
      this.formObject.validate();
  }

```

{% tab template="slider/how-to-04", sourceFiles="app/**/*,index.css", isDefaultActive=true %}

```typescript

import { Component,ViewEncapsulation, OnInit, ViewChild } from '@angular/core';
import { SliderComponent } from '@syncfusion/ej2-angular-inputs';
import { FormValidator, FormValidatorModel } from '@syncfusion/ej2-inputs';

@Component({
    selector: 'my-app',
    templateUrl: 'app/template.html',
    styleUrls:['index.css'],
    encapsulation: ViewEncapsulation.None

})
export class AppComponent {
    @ViewChild('formId') element:any;
    @ViewChild('default') sliderObj: SliderComponent;
    public formObject: FormValidator;
    public ticks: Object = {
        placement: 'Before',
        largeStep: 20,
        smallStep: 5,
        showSmallTicks: true
    };
    ngAfterViewInit() {
      let options: FormValidatorModel = {
        rules: {
          'slider': {
            validateHidden: true,
            min: [30, "You must select value greater than 30"]
          }
        }
      };

      this.formObject = new FormValidator(this.element.nativeElement, options);
    }

    public btnClick(): void {
      if (this.sliderObj.value < 5) {
        alert("Please select value greater than 30");
      } else {
        alert("Submitted");
        this.element.nativeElement.submit();
      }
    }
    public onChanged(): void {
      this.formObject.validate();
    }
}

```

{% endtab %}
