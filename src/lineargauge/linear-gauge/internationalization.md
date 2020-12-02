# Internationalization

<!-- markdownlint-disable MD013 -->

Linear gauge provide supports for internationalization for below gauge elements.

* Axis label.
* Tooltip

For more information about number and date formatter you can refer
[`internationalization`](http://ej2.syncfusion.com/documentation/base/intl.html).

<!-- markdownlint-disable MD036 -->

**Globalization**

Globalization is the process of designing and developing an component that works in different cultures/locales. Internationalization library is used to globalize number in LinearGauge component
using [`format`](../api/linear-gauge/label/#format-string) property in [`labelStyle`](../api/linear-gauge/label).

**Numeric Format**

In the below example axis labels are `globalized` to EUR.

{% tab template= "linear-gauge/internationalization", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container">
        <e-axes>
            <e-axis [labelStyle]='Label'>
            </e-axis>
        </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent {
    public Label:Object;
    ngOnInit(): void {
        this.label =  {
            format: 'c'
        };
    }
}
```

{% endtab %}