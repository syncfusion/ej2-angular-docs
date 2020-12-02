# Customize Slider Bar

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

{% tab template="slider/bar-customization", sourceFiles="app/**/*,index.css", isDefaultActive=true %}

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
