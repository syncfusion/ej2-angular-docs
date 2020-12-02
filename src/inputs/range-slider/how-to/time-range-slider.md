# Time Range Slider

The time formatting can be achieved same as the date formatting using `renderingTicks` and
`change` events. The process of time formatting is
explained in the below sample.

{% tab template="slider/how-to-02", sourceFiles="app/**/*,index.css", isDefaultActive=true %}

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
