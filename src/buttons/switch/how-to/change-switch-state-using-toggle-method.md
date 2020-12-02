---
title: "Toggle between the states"
component: "Switch"
description: "Angular Switch how to section, customization of Switch bar and handle, change size, name and value in form submit, toggle between the states."
---

# Change switch state using toggle method

This section explains about how to toggle between the switch states using [`toggle`](../../api/switch/#toggle) method.

{% tab template="switch/text", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { SwitchComponent } from '@syncfusion/ej2-angular-buttons';

@Component({
    selector: 'app-root',
    template: `<!-- To Render Switch. -->
               <ejs-switch #switch onLabel="ON" offLabel="OFF" (created)='created($event)'></ejs-switch>`
})

export class AppComponent {
    @ViewChild('switch')
    public switch: SwitchComponent;
    public created() {
        this.switch.toggle();
    }
}
```

{% endtab %}

> Switch triggers [`change`](../../api/switch/#change) event on every state stage to perform custom operations.