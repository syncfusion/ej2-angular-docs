
# Numeric Range Slider

The numeric values can be formatted into different decimal digits or fixed number of whole numbers
or to represent the units.
The Numeric processing is demonstrated below.

{% tab template="slider/how-to-03", sourceFiles="app/**/*,index.css", isDefaultActive=true %}

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
