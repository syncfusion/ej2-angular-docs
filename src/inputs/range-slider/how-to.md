---
title: "Slider How To"
component: "Slider"
description: "Angular Slider how to section, date format slider, time format slider, slider validation, slider limits and customization of slider bar, thumb & ticks."
---

# How To

## Value formatting using slider

### Date Format

The Date formatting can be achieved in `ticks` and `tooltip` using `renderingTicks` and
`tooltipChange` events respectively.
The process of formatting is explained in the below sample.

{% tab template="slider/how-to-01", sourceFiles="app/**/*,index.css", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'my-app',
    templateUrl: 'app/template.html',
    styleUrls:['index.css']
})

export class AppComponent {
    public tooltipData: Object = { placement: 'Before', isVisible: true };
    public ticksData: Object = { placement: 'After', largeStep: 2 * 86400000 };
    public min: number = new Date("2013-06-13").getTime();
    public max: number = new Date("2013-06-21").getTime();
    public step: number = 86400000;
    public value: number = new Date("2013-06-15").getTime();

    tooltipChangeHandler(args: SliderTooltipEventArgs): void {
        let totalMiliSeconds = Number(args.text);
        // Converting the current milliseconds to the respective date in desired format
        let custom = { year: "numeric", month: "short", day: "numeric" };
        args.text = new Date(totalMiliSeconds).toLocaleDateString("en-us", custom);
    }

    renderingTicksHandler(args: SliderTickEventArgs): void {
        let totalMiliSeconds = Number(args.value);
        // Converting the current milliseconds to the respective date in desired format
        let custom = { year: "numeric", month: "short", day: "numeric" };
        args.text = new Date(totalMiliSeconds).toLocaleDateString("en-us", custom);
    }
}

```

{% endtab %}

### Time Format

The time formatting can be achieved same as the date formatting using `renderingTicks` and
`change` events. The process of time formatting is
explained in the below sample.

{% tab template="slider/how-to-02", sourceFiles="app/**/*", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'my-app',
    templateUrl: 'app/template.html',
    styleUrls:['index.css']
})

export class AppComponent {
    public tooltipData: Object = { placement: 'Before', isVisible: true };
    public ticksData: Object = { placement: 'After', largeStep: 2 * 3600000 };
    public min: number =new Date(2013, 6, 13, 11).getTime();
    public max: number = new Date(2013, 6, 13, 17).getTime();
    public step: number = 3600000;
    public value: number = new Date(2013, 6, 13, 13).getTime();

    tooltipChangeHandler(args: SliderTooltipEventArgs): void {
        let totalMiliSeconds = Number(args.text);
        let custom = { hour: '2-digit', minute: '2-digit' };
        args.text = new Date(totalMiliSeconds).toLocaleTimeString("en-us", custom);
    }

    renderingTicksHandler(args: SliderTickEventArgs): void {
        let totalMiliSeconds = Number(args.value);
        let custom = { hour: '2-digit', minute: '2-digit' };
        args.text = new Date(totalMiliSeconds).toLocaleTimeString("en-us", custom);
    }
}

```

{% endtab %}

### Numeric Value Customization

The numeric values can be formatted into different decimal digits or fixed number of whole numbers
or to represent the units.
The Numeric processing is demonstrated below.

{% tab template="slider/how-to-03", sourceFiles="app/**/*", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'my-app',
    templateUrl: 'app/template.html',
    styleUrls:['index.css']
})

export class AppComponent {
    public tooltipData01: Object = { isVisible: true, format: '##.## Km' };
    public ticksData01: Object = { placement: 'After', format: '##.## Km', largeStep: 20, smallStep: 10, showSmallTicks: true };

    public tooltipData02: Object = { isVisible: true, format: '##.#00' };
    public ticksData02: Object = { placement: 'After', format: '##.#00', largeStep: 0.02, smallStep: 0.01, showSmallTicks: true };

    public tooltipData03: Object = { isVisible: true, format: '00##' };
    public ticksData03: Object = { placement: 'After', format: '00##', largeStep: 20, smallStep: 10, showSmallTicks: true };

}

```

{% endtab %}

## Slider with ngModel

Slider component supports one and two-way property binding. Slider two way binding can be
achieved through [ngModel](https://angular.io/api/forms/NgModel) Angular directive.

Follow the below steps to perform two-way binding with ngModel.

* Create simple
[slider](https://ej2.syncfusion.com/angular/documentation/slider/getting-started.html#types)
component and binds the value property using ngModel. Refer to the below code snippet.

```html

<ejs-slider class="form-control" id='slider' [ticks]="ticks" [(ngModel)]="slidervalue" name="slider" required #slider="ngModel"></ejs-slider>

```

* Create numeric text box and bind the value using ngModel.

```html

<input type="number" id="name" name="name" class="form-control" required [(ngModel)]="slidervalue" #slider="ngModel">

```

* And name the same variable name in both slider and numeric text box. Which will help to view
the two-way binding i.e. changing value in slider will change the numeric textbox value and vice versa.

* Initialize the value of the variable in component file, while will be bound to slider and text
box initially. The values will be changed synchronously while changing any one (slider or text-box) value.

```typescript

export class AppComponent {
    slidervalue = "30";
  public ticks: Object = {
    placement: 'Before',
    largeStep: 20,
    smallStep: 5,
    showSmallTicks: true
  };
}

```

{% tab template="slider/ngmodel", sourceFiles="app/**/*", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';
import { FormGroup } from '@angular/forms';

@Component({
    selector: 'my-app',
    templateUrl: 'app/template.html',
    styleUrls:['index.css']
})

export class AppComponent {
    slidervalue = "30";
  public ticks: Object = {
    placement: 'Before',
    largeStep: 20,
    smallStep: 5,
    showSmallTicks: true
  };
}

```

{% endtab %}

## Slider in Angular reactive form

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

{% tab template="slider/reactiveform", sourceFiles="app/**/*", isDefaultActive=true %}

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

## Slider validation using Template-driven Forms

Slider can be validated in Angular using [Template-driven](https://angular.io/guide/form-validation#template-driven-validation)
forms.

* The following [CSS classes](https://angular.io/guide/forms#track-control-state-and-validity-with-ngmodel) will be added on Slider component based on the action done by user.

| **Class if true** | **Class if false** | **state** |
| --- | --- | --- |
| `ng-touched` | `ng-untouched` |The control has been visited. |
| `ng-dirty` | `ng-pristine` |The control's value has changed. |
| `ng-valid` | `ng-invalid` |The control's value is valid. |

{% tab template="slider/templateform", sourceFiles="app/**/*", isDefaultActive=true %}

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
  @ViewChild('sliderForm') form: NgForm;
     onSubmit() {
       this.validated = true;
       console.log(this.form.valid)
  }

  ngOnInit() {
   public value =70;
 }
}

```

{% endtab %}

## Slider validation using FormValidator

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

{% tab template="slider/how-to-04", sourceFiles="app/**/*", isDefaultActive=true %}

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

## Customize the bar

Slider appearance can be customized through CSS. By overriding the slider CSS classes, you can
customize the slider bar. The slider bar can be customized with different themes. By default, slider
have class name `e-slider-track` for bar. The class can be overridden with our own color values like
the following code snippet.

```css

.e-control.e-slider .e-slider-track .e-range {
           background: linear-gradient(left, #e1451d 0, #fdff47 17%, #86f9fe 50%, #2900f8 65%, #6e00f8 74%, #e33df9 83%, #e14423 100%);
}

```

You can also apply background color for a certain range depending upon slider values, using change event.

```typescript

change(args: SliderChangeEventArgs) => {
        if (args.value > 0 && args.value <= 25) {
            // Change handle and range bar color to green when
            (sliderHandle as HTMLElement).style.backgroundColor = 'green';
            (sliderTrack as HTMLElement).style.backgroundColor = 'green';
        } else if (args.value > 25 && args.value <= 50) {
            // Change handle and range bar color to royal blue
            (sliderHandle as HTMLElement).style.backgroundColor = 'royalblue';
            (sliderTrack as HTMLElement).style.backgroundColor = 'royalblue';
        } else if (args.value > 50 && args.value <= 75) {
            // Change handle and range bar color to dark orange
            (sliderHandle as HTMLElement).style.backgroundColor = 'darkorange';
            (sliderTrack as HTMLElement).style.backgroundColor = 'darkorange';
        } else if (args.value > 75 && args.value <= 100) {
            // Change handle and range bar color to red
            (sliderHandle as HTMLElement).style.backgroundColor = 'red';
            (sliderTrack as HTMLElement).style.backgroundColor = 'red';
        }
    }

```

{% tab template="slider/bar-customization", sourceFiles="app/**/*", isDefaultActive=true %}

```typescript

import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { SliderComponent, SliderChangeEventArgs } from '@syncfusion/ej2-angular-inputs';

@Component({
    selector: 'my-app',
    template: ` <div class="slider_container">
            <div class="slider-labeltext slider_userselect">Height</div>
            <!-- Square slider element -->
            <ejs-slider id='height_slider' [value]='value' [min]='min' [max]='max' ></ejs-slider>
        </div>
        <div class="slider_container">
            <div class="slider-labeltext slider_userselect">Gradient color</div>
            <ejs-slider id='gradient_slider' [value]='gradient_value' [min]='min' [max]='max' [type]='range' ></ejs-slider>
        </div>
        <div class="slider_container">
            <div class="slider-labeltext slider_userselect">Dynamic thumb and selection bar color</div>
            <ejs-slider id='dynamic_color_slider' [value]='dynamic_value' [min]='min' [max]='max' [type]='range' (created)='created()' (change)='change($event)'></ejs-slider>
        </div>`,
    styleUrls : ["app/app.component.css"],
    encapsulation: ViewEncapsulation.None
})

export class AppComponent {
    public value: number = 30;
    public min: number = 0;
    public max: number = 100;
    public gradient_value: number = 30;
    public range: string = 'MinRange';
    public sliderTrack: HTMLElement;
    public sliderHandle: HTMLElement;
    public dynamic_value: number = 30;
    // Handler used for slider created event
    created() {
        this.sliderTrack = document.getElementById('dynamic_color_slider').querySelector('.e-range');
        this.sliderHandle = document.getElementById('dynamic_color_slider').querySelector('.e-handle');
        (this.sliderHandle as HTMLElement).style.backgroundColor = 'green';
        (this.sliderTrack as HTMLElement).style.backgroundColor = 'green';
    }
    // Handler used for slider change event
    change(args: SliderChangeEventArgs) {
        if (args.value > 0 && args.value <= 25) {
            // Change handle and range bar color to green when
            (this.sliderHandle as HTMLElement).style.backgroundColor = 'green';
            (this.sliderTrack as HTMLElement).style.backgroundColor = 'green';
        } else if (args.value > 25 && args.value <= 50) {
            // Change handle and range bar color to royal blue
            (this.sliderHandle as HTMLElement).style.backgroundColor = 'royalblue';
            (this.sliderTrack as HTMLElement).style.backgroundColor = 'royalblue';
        } else if (args.value > 50 && args.value <= 75) {
            // Change handle and range bar color to dark orange
            (this.sliderHandle as HTMLElement).style.backgroundColor = 'darkorange';
            (this.sliderTrack as HTMLElement).style.backgroundColor = 'darkorange';
        } else if (args.value > 75 && args.value <= 100) {
            // Change handle and range bar color to red
            (this.sliderHandle as HTMLElement).style.backgroundColor = 'red';
            (this.sliderTrack as HTMLElement).style.backgroundColor = 'red';
        }
    }
}

```

{% endtab %}

## Customize the limits

Slider appearance can be customized via CSS. By overriding the slider CSS classes, the slider
limit bar can be customized. Here, the limit bar is customized with different background color. By
default, the slider has class `e-limits` for limits bar. You can override the class with our own
color values as given in the following code snippet.

```css

.e-slider-container.e-horizontal .e-limits {
     background-color: rgba(69, 100, 233, 0.46);
}

```

{% tab template="slider/limits-customization", sourceFiles="app/**/*", isDefaultActive=true %}

```typescript

import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { SliderModule, SliderComponent, LimitDataModel, SliderType, TicksDataModel, TooltipDataModel } from '@syncfusion/ej2-angular-inputs';
import { SliderTooltipEventArgs, SliderTickEventArgs } from '@syncfusion/ej2-inputs';

@Component({
    selector: 'my-app',
    template: ` <div class='sliderwrap'>
            <label class="labeltext">MinRange Slider With Limits</label>
            <ejs-slider id='minrange' #minrange [value]='minValue' [min]='min' [max]='max' [tooltip]='tooltip' [ticks]='ticks' [type]='minType'
                [limits]='minRangeLimits'></ejs-slider>
        </div>
        <div class='sliderwrap'>
            <label class="labeltext">Range Slider With Limits</label>
            <ejs-slider id='range' #range [value]='rangeValue' [min]='min' [max]='max' [tooltip]='tooltip' [ticks]='ticks' [type]='rangetype'
                [limits]='rangeLimits'></ejs-slider>
        </div>`,
   styleUrls : ["app/app.component.css"]
})
export class AppComponent {
    @ViewChild('minrange')
    public minrangeObj: SliderComponent;
    @ViewChild('range')
    public rangeObj: SliderComponent;

    public min: number = 0;
    public max: number = 100;

    public minValue: number = 30;
    public rangeValue: number[] = [30, 70];

    public tooltip: TooltipDataModel = {
        placement: 'Before',
        isVisible: true
    };
    public ticks: TicksDataModel = {
        placement: 'After',
        largeStep: 20,
        smallStep: 5,
        showSmallTicks: true
    };

    public minType: SliderType = 'MinRange';
    public rangetype: SliderType = 'Range';

    public minRangeLimits: LimitDataModel = { enabled: true, minStart: 10, minEnd: 40 };
    public rangeLimits: LimitDataModel = { enabled: true, minStart: 10, minEnd: 40, maxStart: 60, maxEnd: 90 };

    // Eventlisteners to lock first handle of the both sliders
    public fixOne(args: any): void {
        this.minrangeObj.limits.startHandleFixed = args.checked;
        this.rangeObj.limits.startHandleFixed = args.checked;
    }

    // Eventlisteners to lock second handle of the both sliders
    public fixSecond(args: any): void {
        this.minrangeObj.limits.endHandleFixed = args.checked;
        this.rangeObj.limits.endHandleFixed = args.checked;
    }

    // Eventlisteners to change limit values for both sliders
    public minStartChange(args: any): void {
        this.minrangeObj.limits.minStart = args.value;
        this.rangeObj.limits.minStart = args.value;
    }

    public minEndChange(args: any): void {
        this.minrangeObj.limits.minEnd = args.value;
        this.rangeObj.limits.minEnd = args.value;
    }

    public maxStartChange(args: any): void {
        this.minrangeObj.limits.maxStart = args.value;
        this.rangeObj.limits.maxStart = args.value;
    }

    public maxEndChange(args: any): void {
        this.minrangeObj.limits.maxEnd = args.value;
        this.rangeObj.limits.maxEnd = args.value;
    }
}

```

{% endtab %}

## Customize the ticks

Slider view can be customized via CSS. By overriding the slider CSS classes, you can customize the
ticks. The ticks in slider allows you to easily identify the current value/values of the slider. It
contains [`smallStep`](https://ej2.syncfusion.com/angular/documentation/slider/api-ticksData.html#smallstep)
and [`largeStep`](https://ej2.syncfusion.com/angular/documentation/slider/api-ticksData.html#largestep). By
default, slider has class `e-tick` for slider ticks. You can override the class as per your requirement.
Refer to the following code snippet to render ticks.

```typescript

.e-scale .e-tick.e-custom::before {
    content: '\e967';
    position: absolute;
}

```

Here, the color for rendered ticks has been applied through nth-child(`child_number`). The color is
applied to the value of the `child_number` in the slider.

```typescript

.e-scale :nth-child(1)::before {
    color: red;
}

```

{% tab template="slider/ticks-customization", sourceFiles="app/**/*", isDefaultActive=true %}

```typescript

import { Component, ViewEncapsulation, ViewChild} from '@angular/core';
import { SliderComponent } from '@syncfusion/ej2-angular-inputs';
import { SliderTickRenderedEventArgs, SliderTickEventArgs, Placement } from '@syncfusion/ej2-inputs';

@Component({
    selector: 'my-app',
    template: `<div class="slider_container" id="slider_wrapper">
            <div class="slider_labelText userselect">Dynamic ticks color</div>
            <ejs-slider id='ticks_slider' [value]='value' [min]='min' [max]='max' [type]='type' [step]='step' [ticks]='ticks' (renderingTicks)='renderingTicks($event)' ></ejs-slider>
        </div>
        <div class="slider_container">
            <div class="slider_labelText userselect">Ticks with legends</div>
            <ejs-slider id='slider' [value]='value' [min]='min' [max]='max' [type]='type' [ticks]='slider_ticks' (renderedTicks)='renderedTicks($event)'></ejs-slider>
        </div>`,
    styleUrls : ["app/app.component.css"],
    encapsulation: ViewEncapsulation.None
})

export class AppComponent {
    public count: number = 1;
    public value: number = 30;
    public min: number = 0;
    public max: number = 100;
    public step: number = 5;
    public type: string = 'MinRange';
    public ticks: Object = { placement: 'Before', largeStep: 20 };
    public slider_ticks: Object = { placement: 'Both', largeStep: 20, smallStep: 5 };
    private renderingTicks(args: SliderTickEventArgs) {
        if (args.tickElement.classList.contains('e-large')) {
            args.tickElement.classList.add('e-custom');
        }
    }
    private renderedTicks(args: SliderTickRenderedEventArgs) {
        let li: any = args.ticksWrapper.getElementsByClassName('e-large');
        let remarks: any = ['Very Poor', 'Poor', 'Average', 'Good', 'Very Good', 'Excellent'];
        for (let i: number = 0; i < li.length; ++i) {
            (li[i].querySelectorAll('.e-tick-both')[1] as HTMLElement).innerText = remarks[i];
        }
    }
}

```

{% endtab %}

## Customize the thumb

Slider appearance can be customized through CSS. By overriding the slider CSS classes, you can customize
the thumb. By default, slider has unique class `e-handle` for slider thumb. You can override the following
class as per your requirement. Here, in the sample, the slider thumb has been customized to square, circle,
oval shapes, and background image has also been customized.

```typescript

.e-control.e-slider .e-handle {
    background-image: url('https://ej2.syncfusion.com/demos/src/slider/images/thumb.png');
    background-color: transparent;
    height: 25px;
    width: 25px;
}
/* square slider */
.square_slider.e-control.e-slider .e-handle {
    border-radius: 0%;
    background-color: #f9920b;
    border: 0;
}
/* circle slider */
.circle_slider.e-control.e-slider .e-handle {
    border-radius: 50%;
    background-color: #f9920b;
    border: 0;
}
/* oval slider */
.oval_slider.e-control.e-slider .e-handle {
    height: 25px;
    width: 8px;
    top: 3px;
    border-radius: 15px;
    background-color: #f9920b;
}

```

{% tab template="slider/thumb-customization", sourceFiles="app/**/*", isDefaultActive=true %}

```typescript

import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { SliderComponent } from '@syncfusion/ej2-angular-inputs';

@Component({
    selector: 'my-app',
    template: `
    <div class="slider_container">
            <div class="labelText slider-userselect">Square</div>
            <ejs-slider id='square_slider' [value]='value' [min]='min' [max]='max'></ejs-slider>
        </div>
        <div class="slider_container">
            <div class="labelText slider-userselect">Circle</div>
            <ejs-slider id='circle_slider' [value]='value' [min]='min' [max]='max'></ejs-slider>
        </div>
        <div class="slider_container">
            <div class="labelText slider-userselect">Oval</div>
            <ejs-slider id='oval_slider' [value]='value' [min]='min' [max]='max'></ejs-slider>
        </div>
        <div class="slider_container">
            <div class="labelText slider-userselect">Custom image</div>
            <ejs-slider id='image_slider' [value]='value' [min]='min' [max]='max' [ticks]='ticks'></ejs-slider>
        </div>`,
    styleUrls : ["app/app.component.css"],
    encapsulation: ViewEncapsulation.None
})

export class AppComponent {
    public value: number = 30;
    public min: number = 0;
    public max: number = 100;
    public ticks: Object = {
        placement: 'After'
    };
}

```

{% endtab %}
