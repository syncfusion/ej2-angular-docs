---
title: "How To"
component: "Calendar"
description: "Miscellaneous aspects of customizing the calendar"
---

# Set clear button

The following steps illustrate how to configure `clear` button in Calendar UI.

1. On
[`created`](../../api/calendar#created)
 event of Calendar add the required elements to have clear button. Here we have used div with Essential JS 2 Button component.

2. Use the `e-footer` class to the div tag to act as the footer.

3. Use button to clear the selected date from the calendar.

4. Bind the required event handler to the button tag to clear the value.

Below is the code example.

{% tab template="calendar/how-to", isDefaultActive = "true", sourceFiles="app/**/*.ts,styles.css" %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { CalendarComponent } from '@syncfusion/ej2-angular-calendars';

@Component({
    selector: 'app-root',
    styleUrls: ['styles.css'],
    template: `
        <!-- Bind created event to add the clear button --->
        <ejs-calendar #ejCalendar (created)='onCreate()'></ejs-calendar>
        `
})
export class AppComponent {
    @ViewChild('ejCalendar') ejCalendar: CalendarComponent;
    onCreate() {
        let clearBtn: HTMLElement = document.createElement('button');
        let footerElement: HTMLElement = document.getElementsByClassName('e-footer-container')[0];
        //creates the custom element for clear button
        clearBtn.className = 'e-btn e-clear e-flat';
        clearBtn.textContent = 'Clear';
        footerElement.prepend(clearBtn);
        this.ejCalendar.element.appendChild(footerElement);
        let proxy = this;
        // custom click handler to update the value property with null values.
        document.querySelector('.e-footer-container .e-clear').addEventListener('click', function() {
            proxy.ejCalendar.value = null;
        })
    });
}
```

{% endtab %}
