---
title: "Globalization"
component: "DateTimePicker"
description: "Learn about how to globalize the date time picker component and how to localize the culture related content."
---

# Globalization

Globalization is the combination of internalization and localization. You can adapt the component to
various languages by parsing and formatting the date or
number [`Internationalization`](../base/internationalization/) and also add culture specific customization and translation to the text [`localization`](../base/localization/).

By default, the date format, week, month, time format and meridian names are specific to the `American English` culture. It utilizes the
[`Essential JavaScript 2 Internationalization`](../base/internationalization)
package to parse and format the date object based on the culture by using the official [`UNICODE CLDR`](http://cldr.unicode.org/)
JSON data. It provides the `loadCldr` method to load culture specific CLDR JSON data. To use a different culture other
than `English`, follow the steps below:

* Install the `CLDR-Data` package by using the following command (installs all the CLDR JSON data). To
  know more about CLDR-Data refer to the [`CLDR-Data`](http://cldr.unicode.org/index/cldr-spec/json) link.

```cmd
npm install cldr-data --save
```

Once the package installed, you can find the culture
specific JSON data under the location `\node_modules\cldr-data`.

* Now import the installed CLDR JSON data into the `app.component.ts` file.

* Now use the
[`loadCldr`](http://ej2.syncfusion.com/documentation/base/internationalization#cldr-data-dependencies)
method
to load the culture specific CLDR JSON data
from the installed location to `app.component.ts` file.

* DateTimePicker displayed `Sunday` as the first day of week based on default culture ("en-US"). If you want to display the DateTimePicker with loaded culture’s first day of week, you need to import `weekdata.json` file from the `cldr-data/suppemental` as given in the code example.

```typescript

import { loadCldr } from "@syncfusion/ej2-base";

declare var require: any;

loadCldr(
  require("cldr-data/main/de/numbers.json"),
  require("cldr-data/main/de/ca-gregorian.json"),
  require("cldr-data/supplemental/numberingSystems.json"),
  require("cldr-data/main/de/timeZoneNames.json"),
  require('cldr-data/supplemental/weekdata.json') // To load the culture based first day of week
);
```

> The `Localization` library allows you to localize default text content of the DateTimePicker. The DateTimePicker component has static text for  **today** feature that can be changed to other cultures (Arabic, Deutsch, French, etc.) by defining the
[`locale`](../api/datetimepicker#locale) value and translation object.

Locale keywords |Text
-----|-----
today | Name of the button to choose Today date.
placeholder | Hint to describe expected value in input element.

* Before changing to a culture other than `English`, ensure that locale text for the concerned culture is loaded through `load` method of
  `L10n` class.

```typescript
//Load the L10n, loadCldr from ej2-base
import { loadCldr, L10n } from "@syncfusion/ej2-base";

//load the locale object to set the localized placeholder value
L10n.load({
  de: {
    datetimepicker: {
       placeholder: "Wählen Sie ein Datum und eine Uhrzeit aus",
       today:"heute"
    }
  }
});

```

* Set the culture by using the `locale` property.
In the following code example, the DateTimePicker is initialized in `German` culture with
corresponding localized text.

The following example demonstrates the DateTimePicker in `German` culture.

{% tab template="datetimepicker/localization", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from "@angular/core";
import { DateTimePickerComponent } from "@syncfusion/ej2-angular-calendars";
import { loadCldr, L10n } from "@syncfusion/ej2-base";
// Here we have referred local json files for preview purpose
import * as numberingSystems from "./numberingSystems.json";
import * as gregorian from "./ca-gregorian.json";
import * as numbers from "./numbers.json";
import * as detimeZoneNames from "./timeZoneNames.json";

loadCldr(numberingSystems, gregorian, numbers, detimeZoneNames);

@Component({
  selector: 'app-root',
  template: `<ejs-datetimepicker [value]='date' locale='de'></ejs-datetimepicker>`
})
export class AppComponent {
  public date: Date = new Date("12/11/2017 1:00 AM");
  ngOnInit(): void {
    /*loads the localization text*/
    L10n.load({
      de: {
        datetimepicker: {
          placeholder: "Wählen Sie ein Datum und eine Uhrzeit aus",
          today:"heute"
        }
      }
    });
  }
  constructor() {}
}
```

{% endtab %}

## Right-To-Left

The DateTimePicker supports RTL (right-to-left) functionality for languages like Arabic and Hebrew
to displays the text in the right-to-left direction.
Use`enableRtl` property to set the RTL direction.
The following code example initialize the DateTimePicker component in `Arabic` culture and
also explains how to set the localized text to the placeholder using `load` method of `L10n` class.

{% tab template="datetimepicker/rtl", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';
import { DateTimePickerComponent } from '@syncfusion/ej2-angular-calendars';
import { loadCldr, L10n } from '@syncfusion/ej2-base';
// Here we have referred local json files for preview purpose
import * as numberingSystems from './numberingSystems.json';
import * as gregorian from './ca-gregorian.json';
import * as numbers from './numbers.json';
import * as artimeZoneNames from './timeZoneNames.json';

loadCldr(numberingSystems, gregorian, numbers, artimeZoneNames);

@Component({
    selector: 'app-root',
    template: `<ejs-datetimepicker [enableRtl]='true' locale='ar'></ejs-datetimepicker>`
})

export class AppComponent {
    ngOnInit(): void {
       L10n.load({
        'ar': {
          'datetimepicker': {
              placeholder: 'حدد التاريخ والوقت',
              today: "اليوم"
          }
        }
      });
    }
    constructor() {}
}

```

{% endtab %}