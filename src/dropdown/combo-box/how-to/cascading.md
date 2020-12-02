---
title: "Combo box cascading"
component: "ComboBox"
description: "This section explains cascading of the Syncfusion Angular combo box component."
---

# Configure the cascading ComboBox

The cascading ComboBox is a series of ComboBox, where the value of one ComboBox depends
upon  another's value. This can be configured by using
the [change](../../api/combo-box/#change) event of the parent ComboBox.
Within that change event handler, data has to be loaded to the child ComboBox based on the selected
value of the parent ComboBox.

The following example, shows the cascade behavior of country, state, and city
ComboBox. Here, the `dataBind` method is used to reflect the property changes immediately
to the ComboBox.

{% tab template="combobox/cascading", sourceFiles="app/**/*.ts,cascading.html"  %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { ComboBoxComponent } from '@syncfusion/ej2-angular-dropdowns';
import { Query, DataManager } from '@syncfusion/ej2-data';

@Component({
    selector: 'app-root',
    // specifies the template path for the ComboBox component
    templateUrl: `./cascading.html`
})
export class AppComponent {
    constructor() {
    }
    //define the country ComboBox data
    public countryData: { [key: string]: Object }[] = [
        { CountryName: 'Australia', CountryId: '2' },
        { CountryName: 'United States', CountryId: '1' }
    ];
    //define the state ComboBox data
    public stateData: { [key: string]: Object }[] = [
        { StateName: 'New York', CountryId: '1', StateId: '101' },
        { StateName: 'Virginia ', CountryId: '1', StateId: '102' },
        { StateName: 'Tasmania ', CountryId: '2', StateId: '105' }
    ];
    //define the city ComboBox data
    public cityData: { [key: string]: Object }[] = [
        { CityName: 'Albany', StateId: '101', CityId: 201 },
        { CityName: 'Beacon ', StateId: '101', CityId: 202 },
        { CityName: 'Emporia', StateId: '102', CityId: 206 },
        { CityName: 'Hampton ', StateId: '102', CityId: 205 },
        { CityName: 'Hobart', StateId: '105', CityId: 213 },
        { CityName: 'Launceston ', StateId: '105', CityId: 214 }
    ];
    // maps the appropriate column to fields property for country ComboBox
    public countryFields: Object = { text: 'CountryName', value: 'CountryId' };
    // maps the appropriate column to fields property for state ComboBox
    public stateFields: Object = { text: 'StateName', value: 'StateId' };
    // maps the appropriate column to fields property for city ComboBox
    public cityFields: Object = { text: 'CityName', value: 'CityId' };
    //set the placeholder to country ComboBox input
    public countryWatermark: string = "Select a country";
    //set the placeholder to state ComboBox input
    public stateWatermark: string = "Select a state";
    //set the placeholder to city ComboBox input
    public cityWatermark: string = "Select a city";
    @ViewChild('country')
    // create object for country comboBox
    public countryObj: ComboBoxComponent;
    @ViewChild('state')
    // create object for state comboBox
    public stateObj: ComboBoxComponent;
    @ViewChild('city')
    // create object for city comboBox
    public cityObj: ComboBoxComponent;
    public countryChange(): void {
        let tempQuery: Query = new Query().where('CountryId', 'equal', this.countryObj.value);
        //Query the data source based on country ComboBox selected value
        this.stateObj.query = tempQuery;
        // enable the state ComboBox
        this.stateObj.enabled = true;
        //clear the existing selection.
        this.stateObj.text = null;
        // bind the property changes to state ComboBox
        this.stateObj.dataBind();
        //clear the existing selection in city ComboBox
        this.cityObj.text = null;
        //disabe the city ComboBox
        this.cityObj.enabled = false;
        //bind the property cahnges to City ComboBox
        this.cityObj.dataBind();
    }
    public stateChange(): void {
        // Query the data source based on state ComboBox selected value
        this.cityObj.query = new Query().where('StateId', 'equal', this.stateObj.value);
        // enable the city ComboBox
        this.cityObj.enabled = true;
        //clear the existing selection
        this.cityObj.text = null;
        // bind the property change to city ComboBox
        this.cityObj.dataBind();
    }
}
```

{% endtab %}