---
title: "How To"
component: "DatePicker"
description: "Miscellaneous aspects of customizing the date picker"
---

# Customize the datepicker day header

You can change the format of the day that to be displayed in header using [`dayHeaderFormat`](../../api/datepicker#dayheaderformat) property. By default, the format is `Short`.

You can find the possible formats on below.

| **Name** | **Description** |
|------|---------------------|
| `Short` | Sets the short format of day name (like Su ) in day header. |
| `Narrow` | Sets the single character of day name (like S ) in day header. |
| `Abbreviated` | Sets the min format of day name (like Sun ) in day header. |
| `Wide` | Sets the long format of day name (like Sunday ) in day header. |

{% tab template="datepicker/header-format", isDefaultActive = "true", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { DatePickerComponent } from '@syncfusion/ej2-angular-calendars';
import { DropDownListComponent,ChangeEventArgs } from '@syncfusion/ej2-angular-dropdowns';

@Component({
    selector: 'app-root',
    styleUrls: ['styles.css'],
    template: `
      <div id="container">
            <div id="datepicker">
                <ejs-datepicker #default dayHeaderFormat='Short'></ejs-datepicker>
            </div>
            <div id="format">
                <label class="custom-input-label">Header Format Types</label>
                <div id="wrap">
                    <ejs-dropdownlist id="dayformat" #select [dataSource]='formatData' [(value)]='value' [fields]='fields' [placeholder]='waterMark' (change)='formatHandler($event)'></ejs-dropdownlist>
                </div>
            </div>
        </div>
        `
})

export class AppComponent {
    @ViewChild('default')
    public datepickerObj: DatePickerComponent;
    @ViewChild('select')
    public dayHeaderFormat: DropDownListComponent;
     // define the JSON of data
    public formatData: Object[] = [
        { Id: 'Short', Label: 'Short' },
        { Id: 'Narrow', Label: 'Narrow' },
        { Id: 'Abbreviated', Label: 'Abbreviated' },
        { Id: 'Wide', Label: 'Wide' },
    ];
    public fields: Object = { text: 'Label',value: 'Id' };
    public waterMark: string = 'Select format type';
    public value: string ='Short';
    public formatHandler(args: ChangeEventArgs): void {
        this.datepickerObj.dayHeaderFormat = args.value;

        }
    }
}

```

{% endtab %}
