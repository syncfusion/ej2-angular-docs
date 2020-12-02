# Keyboard Interaction

You can use the following keys to interact with the Calendar.
The component implements the keyboard navigation support by following the
   [WAI-ARIA practices](http://www.w3.org/WAI/PF/aria-practices)

It supports the below list of shortcut keys.

| **Press** | **To do this** |
| --- | --- |
| <kbd>Upper Arrow</kbd>  | Focus the previous week date. |
| <kbd>Down Arrow</kbd>  | Focus the next week date. |
| <kbd>Left Arrow</kbd>  | Focus the previous date. |
| <kbd>Right Arrow</kbd>  | Focus the next date. |
| <kbd>Home</kbd>  | Focus the first date in the month. |
| <kbd>End</kbd>  | Focus the last date in the month. |
| <kbd>Page Up</kbd>  | Focus the same date in the previous month. |
| <kbd>Page Down</kbd>  | Focus the same date in the next month. |
| <kbd>Enter</kbd>  | Select the currently focused date. |
| <kbd>Shift + Page Up</kbd>  | Focus the same date in the previous year. |
| <kbd>Shift + Page Down</kbd>  | Focus the same date in the previous year. |
| <kbd>Control + Upper Arrow</kbd>  | Moves into the inner level of view like month-year, year-decade |
| <kbd>Control + Down Arrow</kbd>  | Moves out from the depth level view like decade-year, year-month |
| <kbd>Control + Home</kbd>  | Focus the starting date in the current year. |
| <kbd>Control + End</kbd>  | Focus the ending date in the current year. |

> To focus the Calendar component use the `alt+t` keys.

{% tab template="calendar/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.ts" %}

```typescript
import { Component,HostListener,ViewChild } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
        <ejs-calendar #ejCalendar [value]='dateValue'></ejs-calendar>
        `
})

export class AppComponent {
   @ViewChild('ejCalendar') ejCalendar: CalendarComponent;
    public dateValue: Date = new Date();
    @HostListener('document:keyup', ['$event'])
  handleKeyboardEvent(event: KeyboardEvent) {
    if (event.altKey && event.keyCode === 84 /* t */) {
        // press alt+t to focus the control.
        this.ejCalendar.element.querySelectorAll('.e-content table')[0].focus();
    }
  }
    constructor() {
    }
}
```

{% endtab %}