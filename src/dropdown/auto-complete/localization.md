---
title: "Autocomplete Localization"
component: "AutoComplete"
description: "This section explains the localization support of the Syncfusion angular autocomplete component."
---

# Localization

The Localization library allows you to localize static text content of the
[noRecordsTemplate](../api/auto-complete/#norecordstemplate)
 and [actionFailureTemplate](../api/auto-complete/#actionfailuretemplate)
&nbsp;property according to the culture currently assigned to the AutoComplete.

| Locale key | en-US (default)  |
|------|------|
| noRecordsTemplate |  No Records Found |
| actionFailureTemplate | The Request Failed |

## Loading translations

To load translation object to your application, use load function of the **L10n** class.

In the following sample, French culture is set to the AutoComplete and no data is loaded. Hence, the
[`noRecordsTemplate`](../api/auto-complete/#norecordstemplate) property displays its text in French culture initially and if the sample
is run offline, the [`actionFailureTemplate`](../api/auto-complete/#actionfailuretemplate) property displays its text appropriately.

{% tab template="autocomplete/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component, OnInit } from '@angular/core';
import { DataManager, ODataV4Adaptor, Query } from '@syncfusion/ej2-data';
import { L10n } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    // specifies the template string for the AutoComplete component
    template: `<ejs-autocomplete id='atcelement' [dataSource]='data' [query]='query' [fields]='fields' [placeholder]='text' [locale]='locale'></ejs-autocomplete>`
})
export class AppComponent implements onInit {
    constructor() {
    }
    //set the placeholder text in french to AutoComplete input
    public text: string = 'Trouver un client';
    // bind remotedata to showcase actionFailureTemplate in offline
    public data: DataManager = new DataManager({
        url: 'https://services.odata.org/V4/Northwind/Northwind.svc/Customers',
        adaptor: new ODataV4Adaptor,
        crossDomain: true
    });
    //map the appropriate columns to fields property
    public fields: Object = { value: 'ContactName' };
    //bind the Query instance to query property
    public query: Query = new Query().select(['ContactName', 'CustomerID']).take(0);
    // set placeholder to AutoComplete input element
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
* [How to bind the data to the autocomplete](./data-binding/)