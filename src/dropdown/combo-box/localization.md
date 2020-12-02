---
title: "Combo box Localization"
component: "ComboBox"
description: "This section explains the localization support of the Syncfusion angular combo box component."
---

# Localization

The Localization library allows you to localize static text content of the
[noRecordsTemplate](../api/combo-box/#norecordstemplate) and [actionFailureTemplate](../api/combo-box/#actionfailuretemplate)
 &nbsp;properties according to the culture currently assigned to the ComboBox.

| Locale key | en-US (default)  |
|------|------|
| noRecordsTemplate |  No records found |
| actionFailureTemplate | The request failed |

## Loading translations

To load translation object to your application, use load function of the **L10n** class.

In the following sample, French culture is set to the ComboBox and no data is loaded. Hence,
the [`noRecordsTemplate`](../api/combo-box/#norecordstemplate) property displays its text in French culture initially, and if the sample is
run offline, the [`actionFailureTemplate`](../api/combo-box/#actionfailuretemplate) property displays its text appropriately.

{% tab template="combobox/getting-started", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { DataManager, ODataV4Adaptor, Query } from '@syncfusion/ej2-data';
import { L10n } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    // specifies the template string for the ComboBox component
    template: `<ejs-combobox id='comboelement' #samples [dataSource]='data' [query]='query' [fields]='fields' [placeholder]='text' [locale]='locale'></ejs-combobox>`
})
export class AppComponent implements onInit {
    constructor() {
    }
    //set the placeholder text in french to ComboBox input
    public text: string = "Sélectionnez un élément";
    // bind remotedata to showcase actionFailureTemplate in offline
    public data: DataManager = new DataManager({
        url: 'https://services.odata.org/V4/Northwind/Northwind.svc/Customers',
        adaptor: new ODataV4Adaptor,
        crossDomain: true
    });
    // map appropriate column
    public fields: Object = { text: 'ContactName', value: 'CustomerID' },
    // take 0 item to showcase noRecordsTemplate property
    public query: Query = new Query().select(['ContactName', 'CustomerID']).take(0);
    //set culture to ComboBox component
    public locale: string = 'fr-BE';
    ngOnInit(): void {
        L10n.load({
            'fr-BE': {
            'dropdowns': {
                    'noRecordsTemplate': "Aucun enregistrement trouvé",
                    'actionFailureTemplate': "Modèle d'échec d'action"
                }
            }
        });
    }
}
```

{% endtab %}

## See Also

* [Accessibility](./accessibility/)
* [How to bind the data to the combobox](./data-binding/)