# Internationalization

Maps provides support for internationalization for the below elements.

* Datalabel
* Tooltip

For more information about number and date formatter you can refer
[`internationalization`](http://ej2.syncfusion.com/documentation/base/intl.html).

<!-- markdownlint-disable MD036 -->
**Globalization**

Globalization is the process of designing and developing an component that works in different
cultures/locales. Internationalization library is used to globalize number, date, time values in
Maps component using [`format`] property in the maps model.

**Numeric Format**

In the below example tooltip is globalized to Deutsch culture.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps, MapTooltip } from '@syncfusion/ej2-angular-maps';
import { usa_map } from 'usa.ts';
import { data } from 'data.ts';
Maps.Inject(MapTooltip);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container'>
    <e-layers>
    <e-layer  [shapeData]= 'shapeData'  [shapePropertyPath]= 'shapePropertyPath' [shapeDataPath]= 'shapeDataPath' [dataSource] = 'dataSource' [shapeSettings] = 'shapeSettings' ></e-layer>
    </e-layers>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    ngOnInit(): void {
        public dataSource: Object[] = data;
        public shapeData: Object = usa_map;
        public shapePropertyPath: String = 'name';
        public shapeDataPath: String= 'name';
        public shapeSettings: Object = {
                colorValuePath: 'population',
                colorMapping: [
                {
                            from: 580000 , to: 2800000, color: '#dae8f1', label: '<3M'
                        },
                        {
                            from: 2800000, to: 5280000, color: '#b0cde1', label: '3-6M'
                        },
                        {
                            from: 5280000, to:  8260000, color: '#90bad8', label: '6-9M'
                        },
                        {
                            from: 8260000, to: 11660000, color: '#6ea7d2', label: '9-12M'
                        },
                        {
                            from: 11660000, to: 19600000, color: '#4c96cb', label: '12-20M'
                        },
                        {
                            from: 19600000, to: 26500000, color: '#3182bd', label: '20-25M'
                        },
                        {
                            from: 26500000, to: 38400000, color: '#004374', label: '>25M'
                        }];
            };
        public tooltipSettings: Object ={
                    visible: true,
                    valuePath: 'population',
                    format: 'State: ${name} <br> Population: ${population}'
                };
   }
}

```

{% endtab %}

```typescript

import { Maps } from '@syncfusion/ej2-maps';
import { Maps } from '@syncfusion/ej2-maps';
import { usMap } from './MapData/USA';
import { electionData } from './MapData/ElectionData';

@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='container' [format]="Format" [titleSettings]="titleSettings" [layers]='layers'>
    <ejs-maps>`
})

export class AppComponent implements OnInit {

 ngOnInit(): void {
        public Format:string = 'c';
        public titleSettings: object = {
         text: 'USA Election Results - 2016',
          titleStyle: {
            size: '16px'
           }
        };
        public layers: object[] = [{
            shapeData: usMap,
            dataSource: electionData,
            shapePropertyPath: 'name',
            shapeDataPath: 'State',
            shapeSettings: {
                colorValuePath: 'Candidate',
                colorMapping: [
                {
                    value: 'Trump', color: '#D84444'
                },
                {
                    value: 'Clinton', color: '#316DB5'
                }]
            },
            tooltipSettings: {
                visible: true,
                valuePath: 'State'
            }
        }];
  }
}

```