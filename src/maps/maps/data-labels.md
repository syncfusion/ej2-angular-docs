---
title: " Data Labels in Angular Maps control | Syncfusion "

component: "Maps"

description: "Learn here all about Data Labels of Syncfusion Angular Maps control and more."
---

# Data labels in Angular Maps control

Data labels provide information to users about the shapes of the Maps control. It can be enabled by setting the [`visible`](../api/maps/dataLabelSettingsModel/#visible) property of the [`dataLabelSettings`](../api/maps/dataLabelSettingsModel/) property to "**true**".

## Adding data labels

To display data labels in the Maps, the [`labelPath`](../api/maps/dataLabelSettingsModel/#labelpath) property of [`dataLabelSettings`](../api/maps/dataLabelSettingsModel/) property must be used. The value of the [`labelPath`](../api/maps/dataLabelSettingsModel/#labelpath) property can be taken from the field name in the shape data or data source. In the following example, the value of the [`labelPath`](../api/maps/dataLabelSettingsModel/#labelpath) property is the field name in the shape data of the Maps layer.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps, DataLabel } from '@syncfusion/ej2-angular-maps';
import { usa_map } from 'usa.ts';

Maps.Inject(DataLabel);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container'>
    <e-layers>
    <e-layer  [shapeData]= 'shapeData' [shapeSettings] = 'shapeSettings' [dataLabelSettings] = 'dataLabelSettings'></e-layer>
    </e-layers>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    ngOnInit(): void {
         public shapeData: Object = usa_map;
         public shapeSettings: Object = {
                autofill: true
            };
        public dataLabelSettings: Object = {
            visible: true,
            labelPath: 'name',
        };
   }
}

```

{% endtab %}

In the following example, the value of [`labelPath`](../api/maps/dataLabelSettingsModel/#labelpath) property is set from the field name in the data source of the layer settings.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps, DataLabel } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';

Maps.Inject(DataLabel);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container'>
    <e-layers>
    <e-layer  [shapeData]= 'shapeData' [shapePropertyPath]='shapePropertyPath' [shapeDataPath]='shapeDataPath' [shapeSettings] = 'shapeSettings' [dataSource]='dataSource' [dataLabelSettings] = 'dataLabelSettings'></e-layer>
    </e-layers>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    ngOnInit(): void {
        public shapeData: Object = world_map;
        public shapePropertyPath: String = 'name';
        public shapeDataPath: String = 'name';
        public dataSource: Object = [
            {"name": "Afghanistan", "value": 53, "countryCode": "AF", "population": "29863010", "color": "red", "density": "119", "continent": "Asia"},
            {"name": "Albania", "value": 117, "countryCode": "AL", "population": "3195000", "color": "Blue", "density": "111", "continent": "Europe"},
            {"name": "Algeria", "value": 15, "countryCode": "DZ", "population": "34895000", "color": "Green", "density": "15", "continent": "Africa"}]
        public shapeSettings: Object = {
            autofill: true
        };
        public dataLabelSettings: Object = {
            visible: true,
            labelPath: "continent",
            smartLabelMode: 'Trim'
        };
    }
}

```

{% endtab %}

## Customization

The following properties are available in the [`dataLabelSettings`](../api/maps/dataLabelSettingsModel/) property to customize the data label of the Maps control.

* [`border`](../api/maps/dataLabelSettingsModel/#border) - To customize the color, width and opacity for the border of the data labels in Maps.
* [`fill`](../api/maps/dataLabelSettingsModel/#fill) - To apply the color of the data labels in Maps.
* [`opacity`](../api/maps/dataLabelSettingsModel/#opacity) - To customize the transparency of the data labels in Maps.
* [`textStyle`](../api/maps/dataLabelSettingsModel/#textstyle) - To customize the text style of the data labels in Maps.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps, DataLabel } from '@syncfusion/ej2-angular-maps';
import { usa_map } from 'usa.ts';

Maps.Inject(DataLabel);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container'>
    <e-layers>
    <e-layer  [shapeData]= 'shapeData' [shapeSettings] = 'shapeSettings' [dataLabelSettings] = 'dataLabelSettings'></e-layer>
    </e-layers>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    ngOnInit(): void {
        public shapeData: Object = usa_map;
        public shapeSettings: Object = {
                autofill: true
            };
        public dataLabelSettings: Object = {
            visible: true,
            labelPath: 'name',
            border: {
                color: 'green',
                width: 2
            },
            fill: 'red',
            opacity: 0.9,
            textStyle: {
                color: 'blue',
                size: '10px',
                fontStyle: 'Sans-serif',
                fontWeight: 'normal',
            }
        };
    }
}

```

{% endtab %}

## Smart labels

The Maps control provides an option to handle the labels when they intersect with the corresponding shape borders using the [`smartLabelMode`](../api/maps/dataLabelSettingsModel/#smartlabelmode) property. The following options are available in the [`smartLabelMode`](../api/maps/dataLabelSettingsModel/#smartlabelmode) property.

* None
* Hide
* Trim

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps, DataLabel } from '@syncfusion/ej2-angular-maps';
import { usa_map } from 'usa.ts';

Maps.Inject(DataLabel);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container'>
    <e-layers>
    <e-layer  [shapeData]= 'shapeData' [shapeSettings] = 'shapeSettings' [dataLabelSettings] = 'dataLabelSettings'></e-layer>
    </e-layers>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    ngOnInit(): void {
        public shapeData: Object = usa_map;
        public shapeSettings: Object = {
            autofill: true
        };
        public dataLabelSettings: Object = {
            visible: true,
            labelPath: 'name',
            smartLabelMode: 'Hide'
        };
    }
}

```

{% endtab %}

## Intersect action

The Maps component provides an option to handle the labels when a label intersects with another label using the [`intersectionAction`](../api/maps/dataLabelSettingsModel/#intersectionaction) property. The following options are available in the [`intersectionAction`](../api/maps/dataLabelSettingsModel/#intersectionaction) property.

* None
* Hide
* Trim

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps, DataLabel } from '@syncfusion/ej2-angular-maps';
import { usa_map } from 'usa.ts';

Maps.Inject(DataLabel);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container'  >
    <e-layers>
    <e-layer  [shapeData]= 'shapeData' [shapeSettings] = 'shapeSettings' [dataLabelSettings] = 'dataLabelSettings'></e-layer>
    </e-layers>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    ngOnInit(): void {
        public shapeData: Object = usa_map;
        public shapeSettings: Object = {
            autofill: true
        };
        public dataLabelSettings: Object = {
            visible: true,
            labelPath: 'name',
            intersectionAction: 'Trim'
        };
    }
}

```

{% endtab %}

## Adding data label as a template

The data label can be added as a template in the Maps component. The [`template`](../api/maps/dataLabelSettingsModel/#template) property of [`dataLabelSettings`](../api/maps/dataLabelSettingsModel) property is used to set the data label as a template. Any text or HTML element can be added as the template in data labels.

> Note: The customization properties of data label, [`smartLabelMode`](../api/maps/dataLabelSettingsModel/#smartlabelmode) and [`intersectionAction`](../api/maps/dataLabelSettingsModel/#intersectionaction) properties are not applicable to [`template`](../api/maps/dataLabelSettingsModel/#template) property. The styles can be applied to the label template using the CSS styles of the template element.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps, DataLabel } from '@syncfusion/ej2-angular-maps';
import { usa_map } from 'usa.ts';

Maps.Inject(DataLabel);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container'>
    <e-layers>
    <e-layer  [shapeData]= 'shapeData' [shapeSettings] = 'shapeSettings' [dataLabelSettings] = 'dataLabelSettings'></e-layer>
    </e-layers>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    ngOnInit(): void {
        public shapeData: Object = usa_map;
        public shapeSettings: Object = {
            autofill: true
        };
        public dataLabelSettings: Object = {
            visible: true,
            template: 'Label'
        };
    }
}

```

{% endtab %}