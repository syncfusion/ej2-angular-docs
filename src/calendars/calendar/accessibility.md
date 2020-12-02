---
title: "Accessibility"
component: "Calendar"
description: "The calendar component support accessibility that helps to access all the features through the keyboard, on-screen readers, or other assertive technology devices."
---

# Accessibility

The Web accessibility defines a way to make web content and web applications
more accessible to disabled people. It especially helps the dynamic content change
and advanced user interface controls developed with Ajax, HTML, JavaScript, and related technologies.

Calendar provides built-in compliance with the
[WAI-ARIA](http://www.w3.org/WAI/PF/aria-practices) specifications. WAI-ARIA
supports is achieved through the attributes
like `aria-label`,`aria-selected`, `aria-disabled`, `aria-activedescendant`
applied for navigation buttons,
disable and active day cells.

It helps to provide the information about the widget
for assistive technology to the disabled person in the
screen reader. Calendar component contains
grid as role and grid cell for each day cell

* **Aria-label** : attribute provides the text label for an object
for the previous and next month element. It helps the screen reader object to read for the assistive purpose.

* **Aria-selected** : attribute indicates the currently selected date of the Calendar component.

* **Aria-disabled** : attribute indicates the disabled state of this Calendar component.

* **Aria-activedescendent** : attribute helps in managing the current active child of the Calendar component.

* **Role** : attributes gives assistive technologies information about how to handle each element in a widget.

* **Grid-cell** : attributes define the individual cell that can be focusable and selectable.

## Keyboard Interaction

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
| <kbd>Shift + Page Down</kbd>  | Focus the same date in the next year. |
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
    if (event.altKey && event.keyCode === 84) {
        // press alt+t to focus the control.
        this.ejCalendar.element.querySelectorAll('.e-content table')[0].focus();
    }
  }
    constructor() {
    }
}
```

{% endtab %}