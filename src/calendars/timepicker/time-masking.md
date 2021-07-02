---
title: "Time masking"
component: "TimePicker"
description: "Miscellaneous aspects of customizing the TimePicker"
---

# Enable the Masked Input

DatePicker has `enableMask` property that provides the option to enable the built-in date masking support. Also, you must inject the MaskedDateTime module to enable the masking support.

{% tab template="timepicker/mask-module", isDefaultActive = "true", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { MaskedDateTimeService } from '@syncfusion/ej2-angular-calendars';

@Component({
    selector: 'app-root',
    template: `
        <ejs-timepicker [enableMask]="enableMaskSupport"></ejs-timepicker>
        `
    providers: [MaskedDateTimeService],
})
export class AppComponent {
    public format: string = "HH:mm";
    public enableMaskSupport: boolean = true;
}

```

{% endtab %}

The mask pattern is defined based on the provided time format to the component. If the format is not specified, the mask pattern is formed based on the default format of the current culture.

| **Keys** | **Actions** |
| --- | --- |
| <kbd>Up / Down arrows</kbd> | To increment and decrement the selected portion of the time. |
| <kbd>Left / Right arrows and Tab</kbd> | To navigate the selection from one portion to next portion |

The following example demonstrates default and custom format of TimePicker component with mask.

{% tab template="timepicker/mask-module", isDefaultActive = "true", sourceFiles="app/**/*.ts,app/**/format.html,styles.css" %}

```typescript

import { Component } from '@angular/core';
import { MaskedDateTimeService } from '@syncfusion/ej2-angular-calendars';
@Component({
    selector: 'app-root',
    templateUrl: './app/format.html`
    providers: [MaskedDateTimeService],
})
export class AppComponent {
constructor( ) {
    }
    public format: string = "hh:mm:ss";
    public enableMaskSupport: boolean = true;
}
```

{% endtab %}

# Configure Mask Placeholder

You can change mask placeholder value through property `maskPlaceholder`. By default , it takes the full name of  time co-ordinates such as `hour`, `minute` and `second`.

While changing to a culture other than `English`, ensure that locale text for the concerned culture is loaded through load method of L10n class for mask placeholder values like below.

```typescript
//Load the L10n from ej2-base
import { L10n } from '@syncfusion/ej2-base';

//load the locale object to set the localized mask placeholder value
L10n.load({
'de': {
    timepicker: { hour: 'Stunde' ,minute: 'Minute', second:'Sekunde' }
}
});

```

The following example demonstrates default and customized mask placeholder value.

{% tab template="timepicker/mask-module", isDefaultActive = "true", sourceFiles="app/**/*.ts,app/**/maskplaceholder.html,styles.css" %}

```typescript

import { Component } from '@angular/core';
import { MaskedDateTimeService } from '@syncfusion/ej2-angular-calendars';
@Component({
    selector: 'app-root',
    templateUrl: './app/maskplaceholder.html`
    providers: [MaskedDateTimeService],
})
export class AppComponent {
constructor( ) {
    }
    public enableMaskSupport: boolean = true;
    public maskPlaceholderValue: Object = {hour: 'h', minute: 'm', second: 's'}
}
```

{% endtab %}
