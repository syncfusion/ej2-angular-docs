---
title: "Multiselect Cascading"
component: "MultiSelect"
description: "This section demonstrates the cascading support of the Syncfusion Angular multiselect component."
---

# Configure the Cascading MultiSelect

The cascading MultiSelect is a series of MultiSelect, where the value of one MultiSelect depends
upon  another's value. This can be configured by using the `change` event of the parent MultiSelect.
Within that change event handler, data has to be loaded to the child MultiSelect based on the selected
value of the parent MultiSelect.

The following example, shows the cascade behavior of country, state, and city
MultiSelect. Here, the `dataBind` method is used to reflect the property changes immediately
to the MultiSelect.

{% tab template="multiselect/cascading", sourceFiles="app/**/*.ts,cascading.html" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { MultiSelectComponent } from '@syncfusion/ej2-angular-dropdowns';
import { Query, DataManager, Predicate } from '@syncfusion/ej2-data';

@Component({
    selector: 'app-root',
    // specifies the template path for MultiSelect component
    templateUrl: `./cascading.html`
})
export class AppComponent {
    constructor() {
    }
    //define the country MultiSelect data
    public countryData: { [key: string]: Object }[] = [
        { countryName: 'Australia', countryId: '2' },
        { countryName: 'United States', countryId: '1' }
    ];
    //define the state MultiSelect data
    public stateData: { [key: string]: Object }[] = [
        { stateName: 'New York', countryId: '1', stateId: '101' },
        { stateName: 'Virginia ', countryId: '1', stateId: '102' },
        { stateName: 'Tasmania ', countryId: '2', stateId: '105' }
    ];
    //define the city MultiSelect data
    public cityData: { [key: string]: Object }[] = [
        { cityName: 'Albany', stateId: '101', cityId: 201 },
        { cityName: 'Beacon ', stateId: '101', cityId: 202 },
        { cityName: 'Emporia', stateId: '102', cityId: 206 },
        { cityName: 'Hampton ', stateId: '102', cityId: 205 },
        { cityName: 'Hobart', stateId: '105', cityId: 213 },
        { cityName: 'Launceston ', stateId: '105', cityId: 214 }
    ];
    // maps the appropriate column to fields property for country MultiSelect
    public countryFields: Object = { text: 'countryName', value: 'countryId' };
    // maps the appropriate column to fields property for state MultiSelect
    public stateFields: Object = { text: 'stateName', value: 'stateId' };
    // maps the appropriate column to fields property for city MultiSelect
    public cityFields: Object = { text: 'cityName', value: 'cityId' };
    //set the placeholder to country MultiSelect input
    public countryWatermark: string = "Select countries";
    //set the placeholder to state MultiSelect input
    public stateWatermark: string = "Select states";
    //set the placeholder to city MultiSelect input
    public cityWatermark: string = "Select cities";
    @ViewChild('country')
    public countryObj: MultiSelectComponent;
    @ViewChild('state')
    public stateObj: MultiSelectComponent;
    @ViewChild('city')
    public cityObj: MultiSelectComponent;
    public countrySelect(): void {
      //Query the data source based on country MultiSelect selected value
        let pred:Predicate;
        if(this.countryObj.value)
            for(var d=0;d<this.countryObj.value.length;d++){
                if(pred)
                    pred.or("countryId",'equal',this.countryObj.value[d]);
                else{
                    pred=new Predicate("countryId",'equal',this.countryObj.value[d]);
                }
        }
        else{
            this.stateObj.setProperties({enabled:false,values:[]});
            this.cityObj.setProperties({enabled:false,values:[]});
            return;
        }
        // enable the state MultiSelect
        this.stateObj.setProperties({query:new Query().where(pred),enabled:true,values:[]});
        //clear the existing selection in city MultiSelect
        this.cityObj.setProperties({enabled:false,values:[]});
    }
    public stateSelect(): void {
         //Query the data source based on country MultiSelect selected value
        let pred:Predicate,temp:any;
        if(this.stateObj.value)
            for(var d=0;d<this.stateObj.value.length;d++){
                if(pred)
                    pred.or("stateId",'equal',this.stateObj.value[d]);
                else{
                    pred=new Predicate("stateId",'equal',this.stateObj.value[d]);
                }
        }
        else{
            this.cityObj.setProperties({enabled:false,values:[]});
            return;
        }
        this.cityObj.setProperties({query:new Query().where(pred),enabled:true,values:[]});
    }
}

```

{% endtab %}
