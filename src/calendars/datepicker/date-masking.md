---
title: "Date Masking"
component: "DatePicker"
description: "Miscellaneous aspects of customizing the date picker"
---

# Enable the Masked Input

The DatePicker has built-in support to masking the date value, when `enableMask` property set as `true`.

To use mask support, inject the MaskedDateTime module in the DatePicker.

{% tab template="datepicker/mask-module", isDefaultActive = "true", sourceFiles="app/**/*.ts" %}

```typescript

import { Component} from '@angular/core';
import { MaskedDateTimeService } from '@syncfusion/ej2-angular-calendars';
@Component({
    selector: 'app-root',
    template: `
        <ejs-datepicker  [enableMask]="enableMaskSupport"></ejs-datepicker>
        `,
    providers: [MaskedDateTimeService],
})
export class AppComponent {
constructor( ) {
    }
    public enableMaskSupport: boolean = true;
}
```

{% endtab %}

The mask pattern is defined based on the provided date format to the component. If the format is not specified, the mask pattern is formed based on the default format of the current culture.

The selected portions of date and time co-ordinates  can  be incremented and decremented using the Up/Down arrow keys. You can also use Right/Left arrow keys to navigate from one segment to another.

The following example demonstrates default and custom format of DatePicker component with mask.

{% tab template="datepicker/mask-module", isDefaultActive = "true", sourceFiles="app/**/*.ts,app/**/format.html,styles.css" %}

```typescript

import { Component } from '@angular/core';
import { MaskedDateTimeService } from '@syncfusion/ej2-angular-calendars';
@Component({
    selector: 'app-root',
    templateUrl: './app/format.html',
    providers: [MaskedDateTimeService],
})
export class AppComponent {
constructor( ) {
    }
    public format: string = "dd/MM/yyyy";
    public enableMaskSupport: boolean = true;
}
```

{% endtab %}

# Configure Mask Placeholder

You can change mask placeholder value through property `maskPlaceholder`. By default , it takes the full name of date and time co-ordinates such as `day`, `month`, `year`, `hour` etc.

While changing to a culture other than `English`, ensure that locale text for the concerned culture is loaded through load method of L10n class for mask placeholder values like below.

```typescript
//Load the L10n from ej2-base
import { L10n } from '@syncfusion/ej2-base';

//load the locale object to set the localized mask placeholder value
L10n.load({
'de': {
    datepicker: { day: 'Tag' , month: 'Monat', year: 'Jahr' }
}
});

```

The following example demonstrates default and customized mask placeholder value.

{% tab template="datepicker/mask-module", isDefaultActive = "true", sourceFiles="app/**/*.ts,app/**/maskplaceholder.html,styles.css" %}

```typescript

import { Component } from '@angular/core';
import { MaskedDateTimeService } from '@syncfusion/ej2-angular-calendars';
@Component({
    selector: 'app-root',
    templateUrl: './app/maskplaceholder.html',
    providers: [MaskedDateTimeService],
})
export class AppComponent {
constructor( ) {
    }
    public enableMaskSupport: boolean = true;
    public maskPlaceholderValue: Object = {day: 'd', month: 'M', year: 'y'}
}
```

{% endtab %}
