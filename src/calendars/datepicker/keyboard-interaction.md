# Keyboard Interaction

You can use the following keys to interact with the DatePicker.
The component implements the keyboard navigation support by following the  [WAI-ARIA practices](http://www.w3.org/WAI/PF/aria-practices).

It supports the below list of shortcut keys.

Input Element

| **Press** | **To do this** |
| --- | --- |
| Alt +  Down Arrow | Opens the popup. |
| Alt +  Up Arrow | Closes the popup.|
| Esc | closes the popup. |

> To know more about Calendar navigation keys refer the Calendar
[keyboard Interaction](http://ej2.syncfusion.com/staging/ej2/documentation/calendar/keyboard-interaction)
section.

To focus the Calendar component use the `alt+t` keys.

{% tab template="datepicker/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.ts" %}

```typescript
import { Component,HostListener,ViewChild } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
        <ejs-datepicker #ejDatePicker [value]='dateValue' placeholder='Enter date'></ejs-datepicker>
        `
})

export class AppComponent {
   @ViewChild('ejDatePicker') ejDatePicker: CalendarComponent;
    public dateValue: Date = new Date();
    @HostListener('document:keyup', ['$event'])
  handleKeyboardEvent(event: KeyboardEvent) {
    if (event.altKey && event.keyCode === 84 /* t */) {
        // press alt+t to focus the control.
        this.ejDatePicker.focusIn();
    }
  }
    constructor() {
    }
}
```

{% endtab %}