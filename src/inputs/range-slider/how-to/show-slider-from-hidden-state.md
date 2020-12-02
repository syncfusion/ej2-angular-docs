# Show Slider from Hidden state

This section demonstrates how-to render the Slider component in hidden state and make it visible in button click. We can initialize Slider in hidden state by setting the display as none.

In the sample, by clicking on the button, we can make the Slider visible from hidden state, and we must also call the [`refresh`](https://ej2.syncfusion.com/javascript/documentation/api/base/component/#refresh) method of the Slider to render it properly based on its original dimensions.

{% tab template="slider/hidden-slider", sourceFiles="app/**/*,index.css" %}

```typescript

import { Component, ViewEncapsulation } from '@angular/core';
import { SliderModule } from '@syncfusion/ej2-angular-inputs';

/**
 * Default sample
 */

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
        let totalMilliSeconds = Number(args.text);
        let custom = { hour: '2-digit', minute: '2-digit' };
        args.text = new Date(totalMilliSeconds).toLocaleTimeString("en-us", custom);
    }

    renderingTicksHandler(args: SliderTickEventArgs): void {
        let totalMilliSeconds = Number(args.value);
        let custom = { hour: '2-digit', minute: '2-digit' };
        args.text = new Date(totalMilliSeconds).toLocaleTimeString("en-us", custom);
    }
    ngOnInit() {
      document.getElementById('element').onclick = () => {
        let slider = document.getElementById("wrap");
        let ticks = document.getElementById("slider");
        slider.style.display = "block";
        ticks.ej2_instances[0].refresh();
    };
    }
}

```

{% endtab %}
