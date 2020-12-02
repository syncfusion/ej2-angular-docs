# Date Selection

You can set or get the currently selected date of the calendar using the
[`value`](https://ej2.syncfusion.com/documentation/api/calendar/#value-date)
property.

The following example demonstrates the Calendar with selected date and
[`change`](https://ej2.syncfusion.com/angular/documentation/api/calendar/changedEventArgs/#changedeventargs) event
to display the selected date value.

{% tab template="calendar/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { CalendarComponent } from '@syncfusion/ej2-angular-calendars';

@Component({
    selector: 'app-root',
    template: `<ejs-calendar #ejCalendar [value]='dateValue' (change)='onChange($event)'></ejs-calendar>
        <p id=output style="margin-left:18%; margin-left: 31%;word-wrap: break-word;"></p>`
})

export class AppComponent {
    @ViewChild('ejCalendar') ejCalendar: CalendarComponent;
    public dateValue: Date = new Date();
    constructor() {
    }
    ngAfterViewInit(): void {
        document.getElementById('output').textContent = "" + this.ejCalendar.value;
    }
    onChange(args) {
        document.getElementById('output').textContent = "" + args.value;
    }
}
```

{% endtab %}