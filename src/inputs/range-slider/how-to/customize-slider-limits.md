# Customize Slider Limits

Slider appearance can be customized via CSS. By overriding the slider CSS classes, the slider
limit bar can be customized. Here, the limit bar is customized with different background color. By
default, the slider has class `e-limits` for limits bar. You can override the class with our own
color values as given in the following code snippet.

```css

.e-slider-container.e-horizontal .e-limits {
     background-color: rgba(69, 100, 233, 0.46);
}

```

{% tab template="slider/limits-customization", sourceFiles="app/**/*,index.css", isDefaultActive=true %}

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
