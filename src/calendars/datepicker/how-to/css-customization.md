---
title: "How To"
component: "DatePicker"
description: "Miscellaneous aspects of customizing the date picker"
---

# CSS customization

To customize DatePicker UI, you can make use of [`cssClass`](../../api/datepicker#cssclass) which will be added to DatePicker component as the root CSS class. With this CSS class, you can override existing styles of DatePicker.

Following is the list of classes that provides flexible way to customize the DateRangePicker component.

| **Class Name** | **Description** |
| --- | --- |
| e-date-wrapper | Applied to DatePicker wrapper element. |
| e-datepicker |  Applied to input element and DatePicker popup element. |
| e-datepicker .e-date-wrapper | Applied to input element only. |
| e-input-group-icon.e-date-icon | Applied to popup icon button. |
| e-float-text | Applied to floating label text element. |
| e-popup | Applied to popup element. |
| e-datepicker.e-popup | Applied to DatePicker popup element only. |
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
| e-footer-container | Applied to the Calendar footer container.|
| e-today | Applied to the Calendar Today Button.|

{% tab template="datepicker/customization", isDefaultActive = "true",  sourceFiles="app/**/*.ts,styles.css" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    styleUrls: ['index.css'],
    template: `<ejs-datepicker [value]='dateValue' [cssClass]='cssClass'  placeholder='Enter date' (renderDayCell)='onRenderCell($event)'></ejs-datepicker>`
})
export class AppComponent {
    public cssClass: string = 'e-custom-style';
}

```

{% endtab %}
