---
title: "How To"
component: "Calendar"
description: "Miscellaneous aspects of customizing the calendar"
---

# Show other months dates

The following example demonstrates how to show dates in other months.

The below styles changes the Calendar's other month dates to visible state from its hidden state.

```css
.e-calendar .e-content tr.e-month-hide {
    display: table-row;
}

.e-calendar .e-content td.e-other-month>span.e-day {
    display: inline-block;
}

.e-calendar .e-content td.e-month-hide,
.e-calendar .e-content td.e-other-month {
    pointer-events: auto;
    touch-action: auto;
}
```

{% tab template="calendar/how-to-othermonth", isDefaultActive = "true", sourceFiles="app/**/*.ts,styles.css" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
        <!-- To show other months date refer the "styles.css". -->
        <ejs-calendar [value]='dateValue'></ejs-calendar>
        `
})
export class AppComponent {
    public dateValue: Date = new Date();
}
```

{% endtab %}