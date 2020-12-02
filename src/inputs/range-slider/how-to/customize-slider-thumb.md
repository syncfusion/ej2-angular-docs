# Customize Slider Thumb

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

{% tab template="slider/thumb-customization", sourceFiles="app/**/*,index.css", isDefaultActive=true %}

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
