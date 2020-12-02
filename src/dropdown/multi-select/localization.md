---
title: "Multiselect Localization"
component: "MultiSelect"
description: "This section explains the localization support of the Syncfusion angular multiselect component."
---

# Localization

The Localization library allows you to localize static text content of the
[noRecordsTemplate](../api/multi-select/#norecordstemplate)
 and [actionFailureTemplate](../api/multi-select/#actionfailuretemplate)
&nbsp;properties according to the culture currently assigned to the MultiSelect.

| Locale key | en-US (default)  |
|------|------|
| noRecordsTemplate |  No records found |
| actionFailureTemplate | The request failed |
| overflowCountTemplate | +${count} more.. |
| actionFailureTemplate | ${count} selected |

## Loading translations

To load translation object to your application, use load function of the **L10n** class.

In the following sample, French culture is set to the MultiSelect and no data is loaded.
Hence, the `noRecordsTemplate` property displays its text in French culture initially,
and if the sample is run offline, the `actionFailureTemplate` property displays its text
appropriately. The `overflowCountTemplate` displays its overflow of the value from MultiSelect and
the `totalCountTemplate` displays its total count of the selected value.

{% tab template="multiselect/getting-started", sourceFiles="app/**/*.ts" %}

```typescript

import { Component,OnInit } from '@angular/core';
import { DataManager, ODataV4Adaptor, Query } from '@syncfusion/ej2-data';
// import L10n class for load function
import { L10n,setCulture } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    // specifies the template string for the MultiSelect component
    template: `<ejs-multiselect id='multiselectelement' [dataSource]='customerData' [query]='query' [fields]='fields' [placeholder]='text' [locale]='locale'></ejs-multiselect>`
})
export class AppComponent implements onInit {
    constructor() {
    }
    //set the placeholder text in french to MultiSelect input
    public text: string = "Sélectionnez un élément";
    // bind remotedata to showcase actionFailureTemplate in offline
    public customerData: DataManager = new DataManager({
        url: 'https://services.odata.org/V4/Northwind/Northwind.svc/Customers',
        adaptor: new ODataV4Adaptor,
        crossDomain: true
    });
    // map appropriate column
    public fields: Object = { text: 'ContactName', value: 'CustomerID' };
    // take 0 item to showcase noRecordsTemplate property
    public query: Query = new Query().select(['ContactName', 'CustomerID']).take(0);
    //set culture to MultiSelect component
    public locale: string = 'fr-BE';
    ngOnInit(): void {
        L10n.load({
            'fr-BE': {
            'dropdowns': {
                    'noRecordsTemplate': "Aucun enregistrement trouvé",
                    'actionFailureTemplate': "Modèle d'échec d'action",
                    'overflowCountTemplate': "+${count} plus..",
                    'totalCountTemplate': "${count} choisi"
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