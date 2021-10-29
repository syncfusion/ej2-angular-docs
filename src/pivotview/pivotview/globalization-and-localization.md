---
title: "Globalization"
component: "Pivot Table"
description: "Learn about how to globalize the pivot table and how to localize the culture related content."
---

# Globalization

Globalization is the combination of Internationalization and localization. You can adapt the component to various languages by parsing and formatting the date or number ([`Internationalization`](https://ej2.syncfusion.com/angular/documentation/common/internationalization/)) & adding culture specific customization and translation to the text ([`Localization`](https://ej2.syncfusion.com/angular/documentation/common/localization/)).

## Internationalization

Internationalization library provides support for formatting and parsing the number, date, and time by using the official [`Unicode CLDR`](http://cldr.unicode.org/) JSON data and also provides the `loadCldr` method to load the culture specific CLDR JSON data.

By default, all the Essential JS 2 component are specific to English culture ('en-US'). If you want to go with the different culture other than English, follow the below steps.

* Install the `CLDR-Data` package by using the below command (it installs the CLDR JSON data). For more information about CLDR-Data, refer to this [link](http://cldr.unicode.org/index/cldr-spec/json).

```cmd
npm install cldr-data --save
```

* Once the package installed, you can find the culture specific JSON data under the location `\node_modules\cldr-data`.

* Download the required locale packages to render the angular Pivot Table component with specified locale. To download the locale definition of angular components, use this [link](https://github.com/syncfusion/ej2-locale).

* Now import the required culture from the installed location to `app.ts` file, like the below code snippets.

```typescript
//import the loadCldr from ej2-base
import { loadCldr} from '@syncfusion/ej2-base';

loadCldr(
    require('cldr-data/supplemental/numberingSystems.json'),
    require('cldr-data/main/fr-CH/ca-gregorian.json'),
    require('cldr-data/main/fr-CH/numbers.json'),
    require('cldr-data/main/fr-CH/timeZoneNames.json'));
```

The Internationalization library is used to globalize number, date, and time values in pivot table component using the `dataSourceSettings.formatSettings` option.

* Set the culture by using the `locale` property.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component } from '@angular/core';
import { L10n, setCulture, setCurrencyCode } from '@syncfusion/ej2-base';
import { IDataOptions, FieldListService, CalculatedFieldService, GroupingBarService } from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',
  providers: [FieldListService, CalculatedFieldService, GroupingBarService],
  // specifies the template string for the pivot table component
  template: `<div style="height: 480px;"><ejs-pivotview #pivotview id='PivotView' height='350' [dataSourceSettings]=dataSourceSettings [width]=width
  allowCalculatedField='true' showGroupingBar='true' locale='de-DE' showFieldList='true'></ejs-pivotview></div>`
})

export class AppComponent {
    public dataSourceSettings: IDataOptions;
    ngOnInit(): void {
        setCulture('de');
        setCurrencyCode('EUR');
        L10n.load({
            'de-DE': {
                'pivotview': {
                    'grandTotal': 'Gesamtsumme',
                    'total': 'Insgesamt',
                    'value': 'Wert',
                    'noValue': 'Kein Wert',
                    'row': 'Zeile',
                    'column': 'Spalte',
                    'collapse': 'Zusammenbruch',
                    'expand': 'Erweitern'
                },
                "pivotfieldlist": {
                    'fieldList': 'Feld Liste',
                    'dropRowPrompt': 'Drop Reihe hier',
                    'dropColPrompt': 'Drop column Hier',
                    'dropValPrompt': 'Drop wert hier',
                    'dropFilterPrompt': 'Drop Filter Hier',
                    'addPrompt': 'Feld hinzufügen',
                    'centerHeader': 'Ziehen Sie die Felder zwischen den Bereichen unten:',
                    'add': 'Hinzufügen',
                    'drag': 'Ziehen',
                    'filters': 'Filter',
                    'rows': 'Zeilen',
                    'columns': 'Spalten',
                    'values': 'Werte',
                    'error': 'Fehler',
                    'dropAction': 'Berechnetes Feld nicht in jeder anderen Region außer Wert Achse sein.',
                    'search': 'Suche',
                    'close': 'Schließen',
                    'cancel': 'Abbrechen',
                    'delete': 'Löschen',
                    'alert': 'Warnung',
                    'warning': 'Warnung',
                    'ok': 'OK',
                    'allFields': 'Alle Felder',
                    'noMatches': 'Keine Treffer'
                }
            }
        });
        this.dataSourceSettings = {
            dataSource: Pivot_Data,
            expandAll: false,
            enableSorting: true,
            columns: [{ name: 'Year', caption: 'Production Year' }, { name: 'Quarter' }],
            values: [{ name: 'Sold', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount' }],
            rows: [{ name: 'Country' }, { name: 'Products' }],
            formatSettings: [{ name: 'Amount', format: 'C2', useGrouping: false,
                minimumSignificantDigits: 1, maximumSignificantDigits: 3, currency: 'EUR' }],
            filters: [],
            calculatedFieldSettings: [{ name: 'Total', formula: '"Sum(Amount)"+"Sum(Sold)"' }]
        };
        this.width = "100%";
    }
 }

```

{% endtab %}

> * In the above sample, `Amount` field is formatted by [`NumberFormatOptions`](https://ej2.syncfusion.com/angular/documentation/common/internationalization/#manipulating-numbers). For date formats, the value strings are formatted by [`DateFormatOptions`](https://ej2.syncfusion.com/angular/documentation/common/internationalization/#manipulating-datetime).
> * By default, `locale` value is `en-US`. If you want to change the `en-US` culture to a different culture, you have to change  the `locale` accordingly.
> * Also, you will find more details about support format string for number formats and data formats [`here`](https://ej2.syncfusion.com/angular/documentation/common/internationalization/#supported-format-string).

### Decimal separators

<!-- markdownlint-disable MD009 -->
The decimal separators of pivot table values varies based on the culture applied to the component. The culture can be set by calling the method [`setCulture`](https://ej2.syncfusion.com/angular/documentation/common/internationalization/#setting-global-culture) with appropriate culture string as its parameter. 

The following example demonstrates the decimal separators in `Deutsch` culture.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component } from '@angular/core';
import { loadCldr, L10n, setCulture, setCurrencyCode } from '@syncfusion/ej2-base';
import { IDataOptions, FieldListService, CalculatedFieldService, GroupingBarService } from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';
import * as currencies from './currencies.json';
import * as cagregorian from './ca-gregorian.json';
import * as numbers from './numbers.json';
import * as timeZoneNames from './timeZoneNames.json';
import * as numberingSystems from './numberingSystems.json';

loadCldr(currencies, cagregorian, numbers, timeZoneNames, numberingSystems);
setCulture('de');
setCurrencyCode('EUR');

@Component({
  selector: 'app-container',
  providers: [FieldListService, CalculatedFieldService, GroupingBarService],
  // specifies the template string for the pivot table component
  template: `<div style="height: 480px;"><ejs-pivotview #pivotview id='PivotView' height='350' [dataSourceSettings]=dataSourceSettings [width]=width
  allowCalculatedField='true' showGroupingBar='true' locale='de-DE' showFieldList='true'></ejs-pivotview></div>`
})

export class AppComponent {
    public dataSourceSettings: IDataOptions;
    
    ngOnInit(): void {
        
        L10n.load({
            'de-DE': {
                'pivotview': {
                    'grandTotal': 'Gesamtsumme',
                    'total': 'Insgesamt',
                    'value': 'Wert',
                    'noValue': 'Kein Wert',
                    'row': 'Zeile',
                    'column': 'Spalte',
                    'collapse': 'Zusammenbruch',
                    'expand': 'Erweitern'
                },
                "pivotfieldlist": {
                    'fieldList': 'Feld Liste',
                    'dropRowPrompt': 'Drop Reihe hier',
                    'dropColPrompt': 'Drop column Hier',
                    'dropValPrompt': 'Drop wert hier',
                    'dropFilterPrompt': 'Drop Filter Hier',
                    'addPrompt': 'Feld hinzufügen',
                    'centerHeader': 'Ziehen Sie die Felder zwischen den Bereichen unten:',
                    'add': 'Hinzufügen',
                    'drag': 'Ziehen',
                    'filters': 'Filter',
                    'rows': 'Zeilen',
                    'columns': 'Spalten',
                    'values': 'Werte',
                    'error': 'Fehler',
                    'dropAction': 'Berechnetes Feld nicht in jeder anderen Region außer Wert Achse sein.',
                    'search': 'Suche',
                    'close': 'Schließen',
                    'cancel': 'Abbrechen',
                    'delete': 'Löschen',
                    'alert': 'Warnung',
                    'warning': 'Warnung',
                    'ok': 'OK',
                    'allFields': 'Alle Felder',
                    'noMatches': 'Keine Treffer'
                }
            }
        });
        this.dataSourceSettings = {
            dataSource: Pivot_Data,
            columns: [{ name: 'Year', caption: 'Production Year' }, { name: 'Quarter' }],
            values: [{ name: 'Sold', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount' }],
            rows: [{ name: 'Country' }, { name: 'Products' }],
            formatSettings: [{ name: 'Amount', format: 'C2', currency: 'EUR' }],
            filters: [],
            calculatedFieldSettings: [{ name: 'Total', formula: '"Sum(Amount)"+"Sum(Sold)"' }]
        };
        this.width = "100%";
    }
 }

```

{% endtab %}

## Localization

The [`Localization`](https://ej2.syncfusion.com/documentation/common/api-l10n.html) library allows you to localize default text content of the pivot table. The pivot table component has static text on some features (like drop area text, pivot field list title, etc...) that can be changed to other cultures (Arabic, Deutsch, French, etc.) by defining the
`locale` value and translation object.

The following list of properties and its values are used in the pivot table.

Locale keywords |Text
-----|-----
grandTotal | Grand Total
total | Total
value | Value
noValue | No value
row | Row
column | Column
collapse | Collapse
expand | Expand
rowAxisPrompt | Drop row here
columnAxisPrompt | Drop column here
valueAxisPrompt | Drop value here
filterAxisPrompt | Drop filter here
filter | Filter
filtered | Filtered
sort | Sort
filters | Filters
rows | Rows
columns | Columns
values | Values
close | Close
cancel | Cancel
delete | Delete
calculatedField | Calculated Field
createCalculatedField | Create Calculated Field
fieldName | Enter the field name
error | Error
invalidFormula | Invalid formula.
dropText | Example: ("Sum(Order_Count)" + "Sum(In_Stock)") * 250
dropTextMobile | Add fields and edit formula here.
dropAction | Calculated field cannot be place in any other region except value axis.
alert | Alert
warning | Warning
ok | OK
search | Search
drag | Drag
remove | Remove
sum | Sum
average | Average
count | Count
min | Min
max | Max
allFields | All Fields
formula | Formula
addToRow | Add to Row
addToColumn | Add to Column
addToValue | Add to Value
addToFilter | Add to Filter
emptyData | No records to display
fieldExist | A field already exists in this name. Please enter a different name.
confirmText | A calculation field already exists in this name. Do you want to replace it?
noMatches | No matches
format | Summaries values by
edit | Edit
clear | Clear
formulaField | Drag and drop fields to formula
dragField | Drag field to formula

The following list of properties and its values are used in the pivot field list.

Locale keywords |Text
-----|-----
staticFieldList | Pivot Field List
fieldList | Field List
dropFilterPrompt | Drop filter here
dropColPrompt | Drop column here
dropRowPrompt | Drop row here
dropValPrompt | Drop value here
addPrompt | Add field here
adaptiveFieldHeader | Choose field
centerHeader | Drag fields between axes below:
add | add
drag | Drag
filter | Filter
filtered | Filtered
sort | Sort
remove | Remove
filters | Filters
rows | Rows
columns | Columns
values | Values
calculatedField | Calculated Field
createCalculatedField | Create Calculated Field
fieldName | Enter the field name
error | Error
invalidFormula | Invalid formula.
dropText | Example: ("Sum(Order_Count)" + "Sum(In_Stock)") * 250
dropTextMobile | Add fields and edit formula here.
dropAction | Calculated field cannot be place in any other region except value axis.
search | Search
close | Close
cancel | Cancel
delete | Delete
alert | Alert
warning | Warning
ok | OK
sum | Sum
average | Average
count | Count
min | Min
max | Max
allFields | All Fields
formula | Formula
fieldExist | A field already exists in this name. Please enter a different name.
confirmText | A calculation field already exists in this name. Do you want to replace it?
noMatches | No matches
format | Summaries values by
edit | Edit
clear | Clear
formulaField | Drag and drop fields to formula
dragField | Drag field to formula

### Loading Translations

To load translation object in an application, use [`load`](https://ej2.syncfusion.com/documentation/common/api-l10n.html#load) function of the [`L10n`](https://ej2.syncfusion.com/documentation/common/api-l10n.html) class.

The following example demonstrates the pivot table in `Deutsch` culture.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component } from '@angular/core';
import { L10n } from '@syncfusion/ej2-base';
import { IDataOptions, FieldListService, CalculatedFieldService, GroupingBarService } from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',
  providers: [FieldListService, CalculatedFieldService, GroupingBarService],
  // specifies the template string for the pivot table component
  template: `<div style="height: 480px;"><ejs-pivotview #pivotview id='PivotView' height='350' [dataSourceSettings]=dataSourceSettings [width]=width
  allowCalculatedField='true' showGroupingBar='true' locale='de-DE' showFieldList='true'></ejs-pivotview></div>`
})

export class AppComponent {
    public dataSourceSettings: IDataOptions;
    ngOnInit(): void {
        L10n.load({
            'de-DE': {
                'pivotview': {
                    'grandTotal': 'Gesamtsumme',
                    'total': 'Insgesamt',
                    'value': 'Wert',
                    'noValue': 'Kein Wert',
                    'row': 'Zeile',
                    'column': 'Spalte',
                    'collapse': 'Zusammenbruch',
                    'expand': 'Erweitern'
                },
                "pivotfieldlist": {
                    'fieldList': 'Feld Liste',
                    'dropRowPrompt': 'Drop Reihe hier',
                    'dropColPrompt': 'Drop column Hier',
                    'dropValPrompt': 'Drop wert hier',
                    'dropFilterPrompt': 'Drop Filter Hier',
                    'addPrompt': 'Feld hinzufügen',
                    'centerHeader': 'Ziehen Sie die Felder zwischen den Bereichen unten:',
                    'add': 'Hinzufügen',
                    'drag': 'Ziehen',
                    'filters': 'Filter',
                    'rows': 'Zeilen',
                    'columns': 'Spalten',
                    'values': 'Werte',
                    'error': 'Fehler',
                    'dropAction': 'Berechnetes Feld nicht in jeder anderen Region außer Wert Achse sein.',
                    'search': 'Suche',
                    'close': 'Schließen',
                    'cancel': 'Abbrechen',
                    'delete': 'Löschen',
                    'alert': 'Warnung',
                    'warning': 'Warnung',
                    'ok': 'OK',
                    'allFields': 'Alle Felder',
                    'noMatches': 'Keine Treffer'
                }
            }
        });
        this.dataSourceSettings = {
            dataSource: Pivot_Data,
            expandAll: false,
            enableSorting: true,
            columns: [{ name: 'Year', caption: 'Production Year' }, { name: 'Quarter' }],
            values: [{ name: 'Sold', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount' }],
            rows: [{ name: 'Country' }, { name: 'Products' }],
            formatSettings: [{ name: 'Amount', format: 'C0' }],
            filters: [],
            calculatedFieldSettings: [{ name: 'Total', formula: '"Sum(Amount)"+"Sum(Sold)"' }]
        };
        this.width = "100%";
    }
 }

```

{% endtab %}

## Right-to-left (RTL)

RTL provides an option to switch the text direction and layout of the pivot table component from right to left. It improves the user experiences and accessibility for users who use right-to-left languages (Arabic, Farsi, Urdu, etc...). To enable RTL pivot table, set the `enableRtl` property to **true**.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component } from '@angular/core';
import { L10n } from '@syncfusion/ej2-base';
import { IDataOptions, FieldListService, CalculatedFieldService, GroupingBarService } from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',
  providers: [FieldListService, CalculatedFieldService, GroupingBarService],
  // specifies the template string for the pivot table component
  template: `<div style="height: 480px;"><ejs-pivotview #pivotview id='PivotView' [dataSourceSettings]=dataSourceSettings [width]=width
  allowCalculatedField='true' showGroupingBar='true' locale='ar-AE' enableRtl= true showFieldList='true'></ejs-pivotview></div>`
})

export class AppComponent {
    public dataSourceSettings: IDataOptions;
    ngOnInit(): void {
        L10n.load({
            'ar-AE': {
                'pivotview': {
                    'grandTotal': 'المجموع الكلى',
                    'total': 'المجموع',
                    'value': 'القيمة',
                    'noValue': 'لا قيمة لها',
                    'row': 'صف',
                    'column': 'العمود',
                    'collapse': 'الانهيار',
                    'expand': 'توسيع'
                },
                'pivotfieldlist': {
                    'fieldList': 'قائمة الحقول',
                    'dropRowPrompt': 'تراجع الخلاف هنا',
                    'dropColPrompt': 'انخفاض العمود هنا',
                    'dropValPrompt': 'انخفاض قيمة هنا',
                    'dropFilterPrompt': 'انخفاض هنا عامل التصفية',
                    'addPrompt': 'اضافة حقل هنا',
                    'adaptiveFieldHeader': 'اختر الحقل',
                    'centerHeader': 'اسحب المجالات بين المناطق الموضحة ادناه:',
                    'add': 'اضافة',
                    'drag': 'اسحب',
                    'filters': 'عوامل التصفية',
                    'rows': 'الصفوف',
                    'columns': 'الاعمدة',
                    'values': 'قيم',
                    'search': 'البحث',
                    'close': 'قريب',
                    'cancel': 'الغاء',
                    'delete': 'احذف',
                    'alert': 'حالة تاهب قصوى',
                    'warning': 'تحذير',
                    'ok': 'موافق',
                    'allFields': 'جميع الحقول',
                    'noMatches': 'لا مباريات'
                }
            }
        });
        this.dataSourceSettings = {
            dataSource: Pivot_Data,
            expandAll: false,
            enableSorting: true,
            columns: [{ name: 'Year', caption: 'Production Year' }, { name: 'Quarter' }],
            values: [{ name: 'Sold', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount' }],
            rows: [{ name: 'Country' }, { name: 'Products' }],
            formatSettings: [{ name: 'Amount', format: 'C0' }],
            filters: [],
            calculatedFieldSettings: [{ name: 'Total', formula: '"Sum(Amount)"+"Sum(Sold)"' }]
        };
        this.width = "100%";
    }
 }

```

{% endtab %}

## See Also

* [Internationalization](https://ej2.syncfusion.com/angular/documentation/common/internationalization/)
* [Localization](https://ej2.syncfusion.com/angular/documentation/common/localization/)
