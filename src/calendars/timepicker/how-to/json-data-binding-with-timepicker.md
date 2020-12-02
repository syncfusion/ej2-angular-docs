---
title: "How To"
component: "TimePicker"
description: "Miscellaneous aspects of customizing the time picker"
---

# JSON Data binding with TimePicker

In most of the real cases, the model data will be available with JSON format only.
 Here we have showcased TimePicker component by setting JSON string to value property.
In this JSON, we have used ISO formatted date string which is frequently used date format to get proper date and time value without any misreading.
Also our TimePicker component supports the ISO formatted date value, so parsed JSON value can be directly set to TimePicker model.

{% tab template="timepicker/json-bind", isDefaultActive = "true",  sourceFiles="app/**/*.ts,styles.css" %}

```typescript
import { Component } from '@angular/core';

export interface User {
    selectedDate: Date;
}
export interface JSONUser {
    selectedDate: string;
}
@Component({
    selector: 'app-root',
    template: `
    <!-- To Render TimePicker -->
    <ejs-timepicker id="timepicker" width="240px" [(value)]='user.selectedDate' (change)='onChange($event)'></ejs-timepicker>
    <div class="valuestring">
    <b>User model</b>:  <br/>{{user | json }}
    <br/><br/>
    <b>JSON Data</b>: <br/>{{ model_result }}
    <br/><br/>
    </div>`
})
export class AppComponent {
    public user: User;
    public JSONData: JSONUser = JSON.parse('{ "selectedDate": "2018-12-18T08:56:00+00:00"}');
    public model_result: string = JSON.stringify(this.JSONData);

    public ngOnInit() {
        this.user = this.JSONData;
    }
    onChange(args) {
        this.JSONData.selectedDate = args.value;
        this.model_result = JSON.stringify(this.JSONData);
    }
}

```

{% endtab %}