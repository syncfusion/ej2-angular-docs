# State Persistence

The persistence is a process of maintaining the user interacted settings on
page refresh.

In DatePicker, the selected or entered value has to be persisted on page refresh
or navigation to another page. To persist the value set the
[`enablePersistence`](../api/datepicker#enablepersistence) property
 as true

> It persists the value in local storage of the browser.

The following example demonstrates the persistence of selected date on page refresh.

Select or enter a date value and then refresh the page by clicking the button (Refresh). Now the previously selected date will be persisted.

{% tab template="datepicker/state-persistence", isDefaultActive = "true",  sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<button id='btn' (click)='refresh($event)'> Refresh</button><br>
       <br> <ejs-datepicker placeholder='Enter date'></ejs-datepicker>
        `
})

export  class  AppComponent  {
    refresh():void {
        document.location.reload();
    }
    constructor() {
    }
}
```

{% endtab %}