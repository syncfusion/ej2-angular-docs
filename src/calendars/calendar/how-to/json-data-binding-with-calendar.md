---
title: "How To"
component: "Calendar"
description: "Miscellaneous aspects of customizing the calendar"
---

# JSON Data binding with Calendar

In most of the real cases, the model data will be available with JSON format only. Here we have showcased Calendar component by setting JSON string to value property. In this JSON, we have used ISO formatted date string which is frequently used date format to get proper date and time value without any misreading.
Also our Calendar component supports the ISO formatted date value, so parsed JSON value can be directly set to Calendar model.

{% tab template="calendar/json-bind", isDefaultActive = "true",  sourceFiles="app/**/*.ts,styles.css" %}

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
    <!-- To Render Calendar -->
    <ejs-calendar id="calendar" [(value)]='user.selectedDate' (change)='onChange($event)'></ejs-calendar>
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

    constructor() {}
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