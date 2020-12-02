---
title: "Customization"
component: "DateTimePicker"
description: "Date time picker gives complete control to the user to customize overall appearance of the date time picker in their application."
---

# Customization

The DateTimePicker is available for UI customization that can be achieved by using available properties and events in the component.

## Day and Time Cell format

The DateTimePicker is available for UI customization based on your application requirements.
It can be achieved by using [`renderDayCell`](../api/datetimepicker/renderDayCellEventArgs#renderdaycelleventargs)
event that provides an option to customize each day cell on rendering.

The following example disables the weekends of every month by using `renderDayCell` event.

{% tab template="datetimepicker/accessibility", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript

import { Component } from "@angular/core";
import { DateTimePickerComponent } from "@syncfusion/ej2-angular-calendars";

@Component({
  selector: 'app-root',
  template: `<ejs-datetimepicker placeholder='Select a date and time' (renderDayCell)='onRenderCell($event)'></ejs-datetimepicker>`
})
export class AppComponent {
  onRenderCell(args) {
    /*Apply selected format to the component*/
    if (args.date.getDay() == 0 || args.date.getDay() == 6) {
      //sets isDisabled to true to disable the date.
      args.isDisabled = true;
    }
  }
  constructor() {}
}

```

{% endtab %}

## See Also

* [How to disable the DateTimePicker component](./how-to/disable-placeholder-readonly)
* [How to customize the DateTimePicker day header](./how-to/customize-the-datetimepicker-day-header)