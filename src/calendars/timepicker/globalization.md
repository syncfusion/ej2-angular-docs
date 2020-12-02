---
title: "Globalization"
component: "TimePicker"
description: "Learn about how to globalize the time picker component and how to localize the culture related content."
---

# Globalization

Globalization is the combination of internationalization and localization. You can adapt the component to
various languages by means of parsing and formatting the date or
number [`internationalization`](../base/internationalization/) and also add
culture specific customization and translation to the text
[`localization`](../base/localization).

By default, the time format and meridian names are specific to the `American English` culture. It utilizes the
[`Essential JavaScript 2 Internationalization`](../base/internationalization/)
package to parse and format the date object based on the culture by using the official [`UNICODE CLDR`](http://cldr.unicode.org/)
JSON data. It provides the `loadCldr` method to load culture specific CLDR JSON data. To go with the different culture other
than `English`, follow the steps below.

* Install the `CLDR-Data` package by using the following command (it installs all the CLDR JSON data.
To known more about CLDR-Data refer the [`CLDR-Data`](http://cldr.unicode.org/index/cldr-spec/json) link.

```cmd
npm install cldr-data --save
```

* Once the package installed, you can find the culture
specific JSON data under the location `\node_modules\cldr-data`.

* Now import the installed CLDR JSON data into the `app.component.ts` file.

* Now use the
[`loadCldr`](http://ej2.syncfusion.com/documentation/base/internationalization#cldr-data-dependencies)
method
to load the culture specific CLDR JSON data
from the installed location to `app.component.ts` file.

* TimePicker displayed `Sunday` as the first day of week based on default culture ("en-US"). If you want to display the TimePicker with loaded culture’s first day of week, you need to import `weekdata.json` file from the `cldr-data/suppemental` as given in the code example.

```typescript

import { loadCldr } from '@syncfusion/ej2-base';

declare var require: any;

loadCldr(
    require('cldr-data/supplemental/numberingSystems.json'),
    require('cldr-data/main/de/ca-gregorian.json'),
    require('cldr-data/main/de/numbers.json'),
    require('cldr-data/supplemental/weekdata.json') // To load the culture based first day of week
);

```

* Before changing to a culture other than `English`, ensure that the locale text for the concerned culture is loaded through
[`L10n.load`](http://ej2.syncfusion.com/documentation/base/api/l10n/) method.

```typescript

//Load the L10n from ej2-base
import { L10n } from '@syncfusion/ej2-base';

//load the locale object to set the localized placeholder value
L10n.load({
    'de': {
        'timepicker': { placeholder: 'Wählen Sie Zeit' }
    }
});

 ```

* Set the culture by using the
[`locale`](../api/timepicker#locale)
property. In the following code example, the TimePicker component is initialized in `German` culture with corresponding localized text.

```typescript

import { Component } from '@angular/core';
import { L10n, loadCldr } from '@syncfusion/ej2-base';
import { enableRipple } from '@syncfusion/ej2-base';

//enable ripple style
enableRipple(true);

declare var require: any;

loadCldr(
    require('cldr-data/supplemental/numberingSystems.json'),
    require('cldr-data/main/de/ca-gregorian.json'),
    require('cldr-data/main/de/numbers.json')
);

@Component({
    selector: 'app-root',
    template: `
        <ejs-timepicker [locale]='culture'></ejs-timepicker>
        `
})

export class AppComponent {
    public culture: string = 'de';
    constructor() {}
    ngOnInit(): void {
        L10n.load({
            'de': {
                'timepicker': { placeholder: 'Wählen Sie Zeit' }
            }
        });
    }
}

```

The following sample demonstrate the TimePicker component in `German` culture.

{% tab template="timepicker/internationalization", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { loadCldr, L10n } from '@syncfusion/ej2-base';
// Here we have referred local json files for preview purpose
import * as numberingSystems from './numberingSystems.json';
import * as gregorian from './ca-gregorian.json';
import * as numbers from './numbers.json';
import { enableRipple } from '@syncfusion/ej2-base';

//enable ripple style
enableRipple(true);

loadCldr(numberingSystems, gregorian, numbers);

@Component({
    selector: 'app-root',
    template: `
        <ejs-timepicker [locale]='locale' [value]='dateValue'></ejs-timepicker>
        `
})

export class AppComponent {
    public locale: string = 'de';
    public dateValue: Date = new Date();
    constructor() {}
    ngOnInit(): void {
        L10n.load({
            'de': {
                'timepicker': { placeholder: 'Wählen Sie Zeit' }
            }
        });
    }
}

```

{% endtab %}

## Right-To-Left

The TimePicker supports RTL (right-to-left) functionality for languages like Arabic and Hebrew to displays the
text in the right-to-left direction. Use
[`enableRtl`](../api/timepicker#enablertl)
property to set the RTL direction.

The following code example demonstrates the TimePicker component in `Arabic` culture. It also explains how to set localized text to
the placeholder using [`L10n.load`](http://ej2.syncfusion.com/documentation/base/api/l10n) method.

```typescript

import { Component } from '@angular/core';
import { L10n, loadCldr } from '@syncfusion/ej2-base';
import { enableRipple } from '@syncfusion/ej2-base';

//enable ripple style
enableRipple(true);

declare var require: any;

loadCldr(
    require('cldr-data/supplemental/numberingSystems.json'),
    require('cldr-data/main/ar/ca-gregorian.json'),
    require('cldr-data/main/ar/numbers.json')
);

@Component({
    selector: 'app-root',
    template: `
        <ejs-timepicker [locale]='culture' [enableRtl]='isRTL' [value]='dateValue'></ejs-timepicker>
        `
})

export class AppComponent {
    public culture: string = 'ar';
    public isRTL: boolean = true;
    public dateValue: Date = new Date();
    constructor() {
    }
    ngOnInit(): void {
        L10n.load({
            'ar': {
                'timepicker': { placeholder: 'حدد الوقت' }
            }
        });
    }
}

```

The following example demonstrates TimePicker in `Arabic` culture with right-to-left direction.

{% tab template="timepicker/rtl", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { loadCldr, L10n } from '@syncfusion/ej2-base';
// Here we have referred local json files for preview purpose
import * as numberingSystems from './numberingSystems.json';
import * as gregorian from './ca-gregorian.json';
import * as numbers from './numbers.json';
import { enableRipple } from '@syncfusion/ej2-base';

//enable ripple style
enableRipple(true);

loadCldr(numberingSystems, gregorian, numbers);

@Component({
    selector: 'app-root',
    template: `
        <ejs-timepicker [locale]='locale' [enableRtl]='isRTL' [value]='dateValue'></ejs-timepicker>
        `
})

export class AppComponent {
    public locale: string = 'ar';
    public isRTL: boolean = true;
    public dateValue: Date = new Date();
    constructor() {
    }
    ngOnInit(): void {
        L10n.load({
            'ar': {
                'timepicker': { placeholder: 'حدد الوقت' }
            }
        });
    }
}

```

{% endtab %}