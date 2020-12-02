# Date Range Slider

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
