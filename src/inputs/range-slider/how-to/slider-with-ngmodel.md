# Slider with ngModel

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

{% tab template="slider/ngmodel", sourceFiles="app/**/*,index.css", isDefaultActive=true %}

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
