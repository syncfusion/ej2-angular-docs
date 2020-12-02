---
title: "Globalization"
component: "DateRangePicker"
description: "Learn about how to globalize the date range picker component and how to localize the culture related content."
---

# Globalization

Globalization is the combination of internalization and localization. You can adapt the component to
various languages by parsing and formatting the date or
number [`Internationalization`](../base/internationalization/) and also add culture specific customization and translation to the text [`localization`](../base/localization).

By default, DateRangePicker date format, week, and month names are specific to the English culture. It utilizes the
[`Essential JavaScript 2 Internationalization`](http://ej2.syncfusion.com/documentation/base/internationalization)
package to parse and format the date object based on the culture by using the official [`UNICODE CLDR`](http://cldr.unicode.org/)
JSON data. It provides the `loadCldr` method to load the culture specific CLDR JSON data. To go with the different culture other
than `English`, follow the below steps.

* Install the `CLDR-Data` package by using the below command (it installs all the CLDR JSON data). To
know about CLDR-Data refer the [`CLDR-Data`](http://cldr.unicode.org/index/cldr-spec/json) link.

```cmd
npm install cldr-data --save
```

Once the package installed, you can find the culture specific JSON data under the location `\node_modules\cldr-data`.

* Now import the installed CLDR JSON data into the `app.component.ts` file.

* Now use the
[`loadCldr`](http://ej2.syncfusion.com/documentation/base/internationalization#cldr-data-dependencies)
method
to load the culture specific CLDR JSON data
from the installed location to `app.component.ts` file.

* DateRangePicker displayed `Sunday` as the first day of week based on default culture ("en-US"). If you want to display the DateRangePicker with loaded culture’s first day of week, you need to import `weekdata.json` file from the `cldr-data/suppemental` as given in the code example.

```typescript

import { loadCldr } from '@syncfusion/ej2-base';

declare var require: any;

loadCldr(
    require('cldr-data/supplemental/numberingSystems.json'),
    require('cldr-data/main/de/ca-gregorian.json'),
    require('cldr-data/main/de/numbers.json'),
    require('cldr-data/main/de/timeZoneNames.json'),
    require('cldr-data/supplemental/weekdata.json') // To load the culture based first day of week
);

```

> The `Localization` library allows you to localize default text content of the DateRangePicker. The DateRangePicker component has static text for  **today** feature that can be changed to other cultures (Arabic, Deutsch, French, etc.) by defining the
[`locale`](../api/daterangepicker#locale) value and translation object.

Locale keywords |Text
-----|-----
placeholder | Hint to describe expected value in input element.
startLabel | Label to represent the start date.
endLabel | Label to represent the end date.
applyText | Text present in the apply button.
cancelText | Text present in the cancel button.
selectedDays | Text to represent selected days.
days | Text represents days.
customRange | Text present in the custom range button in presets container.

* Before changing a culture other than `English`, ensure that locale text for the concern culture is loaded through
[`L10n.load`](http://ej2.syncfusion.com/documentation/base/api/l10n) method.

```typescript

//Load the L10n from ej2-base
import { L10n } from '@syncfusion/ej2-base';

//load the locale object to set the localized placeholder value
L10n.load({
    'de': {
        'daterangepicker': {  placeholder: 'Wählen Sie einen Bereich aus',
    startLabel: 'Wählen Sie Startdatum',
    endLabel: 'Wählen Sie Enddatum',
    applyText: 'Sich bewerben',
    cancelText: 'Stornieren',
    selectedDays: 'Ausgewählte Tage',
    days: 'Tage',
    customRange: 'benutzerdefinierten Bereich'
     }
    }
});

 ```

* Set the culture by using the
[`locale`](../api/daterangepicker#locale)
property. In this below
code example, initialize the DateRangePicker component in `German` culture with
corresponding localized text.

```typescript

import { Component } from '@angular/core';
import { L10n, loadCldr } from '@syncfusion/ej2-base';

declare var require: any;

loadCldr(
    require('cldr-data/supplemental/numberingSystems.json'),
    require('cldr-data/main/de/ca-gregorian.json'),
    require('cldr-data/main/de/numbers.json'),
    require('cldr-data/main/de/timeZoneNames.json')
);

@Component({
    selector: 'app-root',
    template: `
        <ejs-daterangepicker locale='de'></ejs-daterangepicker>
        `
})

export class AppComponent {
    constructor() {
    }
    ngOnInit(): void {
        L10n.load({
            'de': {
                'daterangepicker': {
                    placeholder: 'Wählen Sie einen Bereich aus',
                    today:"heute"
                    startLabel: 'Wählen Sie Startdatum',
                    endLabel: 'Wählen Sie Enddatum',
                    applyText: 'Sich bewerben',
                    cancelText: 'Stornieren',
                    selectedDays: 'Ausgewählte Tage',
                    days: 'Tage',
                    customRange: 'benutzerdefinierten Bereich'
                }
            }
        });
    }
}

```

The following sample demonstrate the DateRangePicker component in `German` culture.

{% tab template="daterangepicker/internationalization", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { loadCldr, L10n } from '@syncfusion/ej2-base';
// Here we have referred local json files for preview purpose
import * as numberingSystems from './numberingSystems.json';
import * as gregorian from './ca-gregorian.json';
import * as numbers from './numbers.json';
import * as detimeZoneNames from './timeZoneNames.json';

loadCldr(numberingSystems, gregorian, numbers, detimeZoneNames);

@Component({
    selector: 'app-root',
    template: `<ejs-daterangepicker locale='de'></ejs-daterangepicker>`
})

export class AppComponent {
    constructor() {
    }
    ngOnInit(): void {
        L10n.load({
            'de': {
                'daterangepicker': { placeholder: 'Wählen Sie einen Bereich aus',
                today:"heute",
                startLabel: 'Wählen Sie Startdatum',
                endLabel: 'Wählen Sie Enddatum',
                applyText: 'Sich bewerben',
                cancelText: 'Stornieren',
                selectedDays: 'Ausgewählte Tage',
                days: 'Tage',
                customRange: 'benutzerdefinierten Bereich'
                }
            }
        });
    }
}

```

{% endtab %}

## Right-To-Left

The DateRangePicker supports RTL (right-to-left) functionality for languages like Arabic, Hebrew to displays the
text in the right-to-left direction. Use
[`enableRtl`](../api/daterangepicker#enablertl)
property to set the RTL direction.

The below code example demonstrates the DateRangePicker component in `Hebrew` culture, also explains how to set the localized text to
the placeholder using [`L10n.load`](http://ej2.syncfusion.com/documentation/base/api/l10n/) method.

```typescript

import { Component } from '@angular/core';
import { L10n, loadCldr } from '@syncfusion/ej2-base';

declare var require: any;

loadCldr(
    require('cldr-data/supplemental/numberingSystems.json'),
    require('cldr-data/main/he/ca-gregorian.json'),
    require('cldr-data/main/he/numbers.json'),
    require('cldr-data/main/he/timeZoneNames.json')
);

@Component({
    selector: 'app-root',
    template: `<ejs-daterangepicker locale='he' [enableRtl]='isRTL'></ejs-daterangepicker>`
})

export class AppComponent {
    public isRTL: boolean = true;
    constructor() {
    }
    ngOnInit(): void {
        L10n.load({
            'he': {
                'daterangepicker': { placeholder: 'בחר טווח',
                today:'היום',
        startLabel: 'תווית התחלה',
        endLabel: 'ח',
        applyText: 'להחיל טקסט',
        cancelText: 'בטל טקסט',
        selectedDays: 'ימים נבחרים',
        days: 'أימים',
        customRange: 'טווח מותאם אישית'
         }
         }
    });
    }
}

```

The following example demonstrates the DateRangePicker in `Hebrew` culture with right-to-left direction.

{% tab template="daterangepicker/rtl", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { loadCldr, L10n } from '@syncfusion/ej2-base';
// Here we have referred local json files for preview purpose
import * as numberingSystems from './numberingSystems.json';
import * as gregorian from './ca-gregorian.json';
import * as numbers from './numbers.json';
import * as hetimeZoneNames from './timeZoneNames.json';

loadCldr(numberingSystems, gregorian, numbers, hetimeZoneNames);

@Component({
    selector: 'app-root',
    template: `<ejs-daterangepicker locale='he' [enableRtl]='isRTL'></ejs-daterangepicker>`
})

export class AppComponent {
    public isRTL: boolean = true;
    constructor() {
    }
    ngOnInit(): void {
        L10n.load({
            'he': {
                'daterangepicker': { placeholder: 'בחר טווח',
                 today:'היום',
        startLabel: 'תווית התחלה',
        endLabel: 'ח',
        applyText: 'להחיל טקסט',
        cancelText: 'בטל טקסט',
        selectedDays: 'ימים נבחרים',
        days: 'أימים',
        customRange: 'טווח מותאם אישית'
         }
        }
    });
}
}

```

{% endtab %}

## Date format customization

Representation of start and end date strings can be customized to required format by using format property.
By default, it will set based on the culture.
To know more about the date format standards, refer to the Internationalization Date Format section.
In below sample, the date strings are formatted to `yyyy-MM-dd` and separator between the date ranges is set to "to".

{% tab template="daterangepicker/getting-started", isDefaultActive = "true",  sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<ejs-daterangepicker [format]='dateFormat' separator='to' placeholder='Select a range'></ejs-daterangepicker>`
})
export class AppComponent {
    public dateFormat: String = "yyyy-MM-dd";
    constructor() {
    }
}

```

{% endtab %}