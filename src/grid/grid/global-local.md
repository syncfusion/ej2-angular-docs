---
title: "Globalization"
component: "Grid"
description: "Learn how to apply localization (l10n), internationalization (i18n), and right-to-left (RTL) in Essential JS 2 DataGrid control."
---

# Globalization

## Localization

The [`Localization`](../common/localization/) library allows you to localize default text content of the Grid.
The grid component has static text on some features (like group drop area text, pager information text, etc.)
that can be changed to other cultures (Arabic, Deutsch, French, etc.) by defining the
[`locale`](../api/grid/#locale) value and translation object.

The following list of properties and its values are used in the grid.

Locale key words |Text
-----|-----
EmptyRecord | No records to display
True | true
False | false
InvalidFilterMessage | Invalid Filter Data
GroupDropArea | Drag a column header here to group its column
UnGroup | Click here to ungroup
GroupDisable | Grouping is disabled for this column
FilterbarTitle | \s filter bar cell
EmptyDataSourceError | DataSource must not be empty at initial load since columns are generated from dataSource in AutoGenerate Column Grid
Add | Add
Edit| Edit
Cancel| Cancel
Update| Update
Delete | Delete
Print | Print
Pdfexport | PDF Export
Excelexport | Excel Export
Wordexport | Word Export
Csvexport | CSV Export
Search | Search
Columnchooser | Columns
Save | Save
Item | item
Items | items
EditOperationAlert | No records selected for edit operation
DeleteOperationAlert | No records selected for delete operation
SaveButton | Save
OKButton | OK
CancelButton | Cancel
EditFormTitle | Details of
AddFormTitle | Add New Record
BatchSaveConfirm | Are you sure you want to save changes?
BatchSaveLostChanges | Unsaved changes will be lost. Are you sure you want to continue?
ConfirmDelete | Are you sure you want to Delete Record?
CancelEdit | Are you sure you want to Cancel the changes?
ChooseColumns | Choose Column
SearchColumns | search columns
Matchs | No Matches Found
FilterButton | Filter
ClearButton | Clear
StartsWith | Starts With
EndsWith | Ends With
Contains | Contains
Equal | Equal
NotEqual | Not Equal
LessThan | Less Than
LessThanOrEqual | Less Than Or Equal
GreaterThan | Greater Than
GreaterThanOrEqual | Greater Than Or Equal
ChooseDate | Choose a Date
EnterValue | Enter the value
Copy | Copy
Group | Group by this column
Ungroup | Ungroup by this column
autoFitAll | AutoFit all columns
autoFit | AutoFit this column
Export | Export
FirstPage | First Page
LastPage | Last Page
PreviousPage | Previous Page
NextPage | Next Page
SortAscending | Sort Ascending
SortDescending | Sort Descending
EditRecord | Edit Record
DeleteRecord | Delete Record
FilterMenu | Filter
SelectAll | Select All
Blanks | Blanks
FilterTrue | True
FilterFalse | False
NoResult | No Matches Found
ClearFilter | Clear Filter
NumberFilter | Number Filters
TextFilter | Text Filters
DateFilter | Date Filters
MatchCase | Match Case
Between | Between
CustomFilter | Custom Filter
CustomFilterPlaceHolder | Enter the value
CustomFilterDatePlaceHolder | Choose a date
AND | AND
OR | OR
ShowRowsWhere | Show rows where:
currentPageInfo | {0} of {1} pages
totalItemsInfo | ({0} items)
totalItemInfo | ({0} item)
firstPageTooltip | Go to first page
lastPageTooltip | Go to last page
nextPageTooltip | Go to next page
previousPageTooltip | Go to previous page
nextPagerTooltip | Go to next pager
previousPagerTooltip | Go to previous pager
pagerDropDown | Items per page
pagerAllDropDown | Items
All | All

### Loading translations

To load translation object in an application use **load** function of **L10n** class.

The below example demonstrates the Grid in **Deutsch** culture.

{% tab template="grid/localization", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { L10n, setCulture } from '@syncfusion/ej2-base';
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { PageSettingsModel } from '@syncfusion/ej2-angular-grids';

setCulture('de-DE');

L10n.load({
    'de-DE': {
        grid: {
            EmptyRecord: 'Keine Aufzeichnungen angezeigt',
            GroupDropArea: 'Ziehen Sie einen Spaltenkopf hier, um die Gruppe ihre Spalte',
            UnGroup: 'Klicken Sie hier, um die Gruppierung aufheben',
EmptyDataSourceError: 'DataSource darf bei der Erstauslastung nicht leer sein, da Spalten aus der dataSource im AutoGenerate Spaltenraster',
            Item: 'Artikel',
            Items: 'Artikel'
        },
        pager: {
            currentPageInfo: '{0} von {1} Seiten',
            totalItemsInfo: '({0} Beiträge)',
            firstPageTooltip: 'Zur ersten Seite',
            lastPageTooltip: 'Zur letzten Seite',
            nextPageTooltip: 'Zur nächsten Seite',
            previousPageTooltip: 'Zurück zur letzten Seit',
            nextPagerTooltip: 'Zum nächsten Pager',
            previousPagerTooltip: 'Zum vorherigen Pager'
        }
    }
});

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [locale]='de-DE' [allowGrouping]='true' [allowPaging]='true'
             [pageSettings]='pageOptions' height='220px'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
               </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public pageOptions: PageSettingsModel;

    ngOnInit(): void {
        this.data = data;
        this.pageOptions = { pageSize: 6 };
    }
}

```

{% endtab %}

## Internationalization

The [`Internationalization`](../common/intl.html) library is used to globalize number, date,
and time values in grid component using format strings in the
[`columns.format`](../api/grid/column/#format).

For importing **json** files in your application, you need to include the **json-typings.d.ts** file.

```typescript
declare module "*.json" {
        const value: any;
        export default value;
    }
```

You need to load culture format files in **ngOnInit** function.

{% tab template="grid/localization", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { L10n, loadCldr, setCulture, setCurrencyCode } from '@syncfusion/ej2-base';
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';

L10n.load({
    'de-DE': {
        grid: {
            EmptyRecord: 'Keine Aufzeichnungen angezeigt',
            GroupDropArea: 'Ziehen Sie einen Spaltenkopf hier, um die Gruppe ihre Spalte',
            UnGroup: 'Klicken Sie hier, um die Gruppierung aufheben',
EmptyDataSourceError: 'DataSource darf bei der Erstauslastung nicht leer sein, da Spalten aus der dataSource im AutoGenerate Spaltenraster',
            Item: 'Artikel',
            Items: 'Artikel'
        },
        pager: {
            currentPageInfo: '{0} von {1} Seiten',
            totalItemsInfo: '({0} Beiträge)',
            firstPageTooltip: 'Zur ersten Seite',
            lastPageTooltip: 'Zur letzten Seite',
            nextPageTooltip: 'Zur nächsten Seite',
            previousPageTooltip: 'Zurück zur letzten Seit',
            nextPagerTooltip: 'Zum nächsten Pager',
            previousPagerTooltip: 'Zum vorherigen Pager'
        }
    }
});

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [locale]='de-DE' height='315px'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='Freight' headerText='Freight' [format]='formatOptions' textAlign='Right' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
               </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public formatOptions: object;

    ngOnInit(): void {
        setCulture('de-DE');
        setCurrencyCode('EUR');

        loadCldr('./currencies.json',
            './numbers.json',
            './ca-gregorian.json',
            './timeZoneNames.json',
            './numberingSystems.json');

        this.data = data;
        this.formatOptions = { format: 'C2', useGrouping: false, minimumSignificantDigits: 1, maximumSignificantDigits: 3, currency: 'EUR' }
    }
}

```

{% endtab %}

> * In the above sample, **Freight** column is formatted by [`NumberFormatOptions`](../common/internationalization/#manipulating-numbers).
> * By default, [`locale`](../api/grid/#locale) value is **en-US**. If you want to change **en-US** culture, then set the [`locale`](../api/grid/#locale).

## Right to Left - RTL

RTL provides an option to switch the text direction and layout of Grid component from right to left.
It improves the user experiences and accessibility for users who use right-to-left languages(Arabic, Farsi, Urdu, etc).
To enable RTL in the Grid, set the [`enableRtl`](../api/grid/#enablertl) to true.

{% tab template="grid/paging1", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { L10n, setCulture } from '@syncfusion/ej2-base';
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import { PageSettingsModel } from '@syncfusion/ej2-angular-grids';

setCulture('ar-AE');

L10n.load({
    'ar-AE': {
        grid: {
            EmptyRecord: 'لا سجلات لعرضها',
            EmptyDataSourceError: 'يجب أن يكون مصدر البيانات فارغة في التحميل الأولي منذ يتم إنشاء الأعمدة من مصدر البيانات في أوتوجينيراتد عمود الشبكة'
        },
        pager: {
            currentPageInfo: '{0} من {1} صفحة',
            totalItemsInfo: '({0} العناصر)',
            firstPageTooltip: 'انتقل إلى الصفحة الأولى',
            lastPageTooltip: 'انتقل إلى الصفحة الأخيرة',
            nextPageTooltip: 'انتقل إلى الصفحة التالية',
            previousPageTooltip: 'انتقل إلى الصفحة السابقة',
            nextPagerTooltip: 'الذهاب إلى بيجر المقبل',
            previousPagerTooltip: 'الذهاب إلى بيجر السابقة'
        }
    }
});

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [enableRtl]='true' [locale]='ar-AE' [allowPaging]='true' [pageSettings]='pageOptions'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
               </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: object[];
    public pageOptions: PageSettingsModel;

    ngOnInit(): void {
        this.data = data;
        this.pageOptions = { pageSize: 7 };
    }
}

```

{% endtab %}

## See Also

* [Internationalization](../common/internationalization)
* [Localization](../common/localization/)