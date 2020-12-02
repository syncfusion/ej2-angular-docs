---
title: "Customization"
component: "DatePicker"
description: "Date picker gives complete control to the user to customize overall appearance of the date picker in their application."
---

# Customization

You can customize the  entire appearance of the input element and Calendar by using
custom
[`cssClass`](../api/datepicker#cssclass)
property.
Also you can use the calendar's
[`renderDayCell`](../api/datepicker/renderDayCellEventArgs#renderdaycelleventargs)
event to customize the appearance of the each day cell.

Below is the list of classes that provides flexible way to customize the DatePicker component.

| **Class Name** | **Description** |
| --- | --- |
| e-date-wrapper | Applied to DatePicker wrapper |
| e-datepicker | Applied to the DatePicker element.|
| e-float-text | Applied to the floating label.  |
| e-date-icon | Applied to the DatePicker icon. |
| e-popup-wrapper | Applied to DatePicker popup wrapper.|
| e-calendar | Applied to Calendar element. |
| e-header | Applied to Calendar header.|
| e-title |Applied to Calendar title. |
| e-icon-container | Applied to Calendar previous and next icon container.|
| e-prev |  Applied to Calendar previous icon.|
| e-next | Applied to Calendar next icon.|
| e-weekend | Applied to Calendar weekend dates.|
| e-other-month |  Applied to Calendar other month dates.|
| e-day | Applied to each day cell of the Calendar.|
| e-selected | Applied to Calendar selected dates.|
| e-disabled | Applied to Calendar disabled dates.|

The following example disables the weekends of every month using `renderDayCell` event.
Here we have used the `e-disabled` class to highlight the disabled date.

{% tab template="datepicker/getting-started", isDefaultActive = "true",  sourceFiles="app/**/*.ts,index.css" %}

```typescript


import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    styleUrls: ['index.css'],
    template: `<ejs-datepicker [value]='dateValue' placeholder='Enter date' (renderDayCell)='onRenderCell($event)'></ejs-datepicker>`
})
export class AppComponent {
    public dateValue:Date = new Date();
    constructor() {
    }
    public  onRenderCell(args: RenderDayCellEventArgs): void {
    if (args.date.getDay() == 0 || args.date.getDay() == 6) {
        //sets isDisabled to true to disable the date.
        args.isDisabled = true;
        //To know about the disabled date customization, you can refer in "styles.css".
    }

}
}

```

{% endtab %}

## See Also

* [Render DatePicker with CSS customization](./how-to/css-customization)
* [How to disable the DatePicker control](./how-to/disable-placeholder-readonly)
* [How to set read-only for DatePicker](./how-to/disable-placeholder-readonly)
* [How to customize the DatePicker day header](./how-to/customize-the-datepicker-day-header)
