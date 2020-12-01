# Localization

Localization library allows you to localize the text content of the Syncfusion Angular UI Components.

## Loading translations

To load a translation object in your application use [`load`](https://ej2.syncfusion.com/documentation/api/base/l10n#load) function of `L10n` class.

{% tab template="common/locale", sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { L10n, setCulture } from '@syncfusion/ej2-base';
import { Component, OnInit } from '@angular/core';
import { data } from './datasource';
import {PageSettingsModel } from '@syncfusion/ej2-angular-grids';

setCulture('de-DE');

L10n.load({
    'de-DE': {
        'grid': {
            'EmptyRecord': 'Keine Aufzeichnungen angezeigt',
            'GroupDropArea': 'Ziehen Sie einen Spaltenkopf hier, um die Gruppe ihre Spalte',
            'UnGroup': 'Klicken Sie hier, um die Gruppierung aufheben',
            'EmptyDataSourceError': 'DataSource darf bei der Erstauslastung nicht leer sein, da Spalten aus der dataSource im AutoGenerate Spaltenraster',
            'Item': 'Artikel',
            'Items': 'Artikel'
        },
        'pager':{
            'currentPageInfo': '{0} von {1} Seiten',
            'totalItemsInfo': '({0} Beiträge)',
            'firstPageTooltip': 'Zur ersten Seite',
            'lastPageTooltip': 'Zur letzten Seite',
            'nextPageTooltip': 'Zur nächsten Seite',
            'previousPageTooltip': 'Zurück zur letzten Seit',
            'nextPagerTooltip': 'Zum nächsten Pager',
            'previousPagerTooltip': 'Zum vorherigen Pager'
        }
    }
});

@Component({
    selector: 'app-root',
    template: `<ejs-grid [dataSource]='data' [locale]='de-DE' [allowGrouping]='true' [allowPaging]='true' [pageSettings]='pageOptions' height='220px'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='Right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
               </ejs-grid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public pageOptions: PageSettingsModel;

    ngOnInit(): void {
        this.data = data;
        this.pageOptions = { pageSize: 6 };
    }
}
```

{% endtab %}

## Changing current locale

Current locale can be changed for all the Syncfusion Angular UI Components in your application by
invoking `setCulture` function with your desired culture name.

```typescript
import {L10n, setCulture} from '@syncfusion/ej2-base';
L10n.load({
    'fr-BE': {
       'Button': {
             'id': 'Numéro de commande',
             'date':'Date de commande'
         }
     }
});
setCulture('fr-BE');
```

>Note: Before changing a culture globally, you need to ensure that locale text for the concern   culture is loaded through `L10n.load` function.
