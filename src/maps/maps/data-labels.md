# Data labels

Data labels provide information to users about the shapes of the Maps component.

## Add data labels

You can add label text to the shapes of the Maps component using `dataLabelSettings`. The following sample demonstrates the names of all the states n the United States in data labels.

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
            };
   }
}

```

{% endtab %}

> The `autofill` property is used in `shapeSettings` to apply the default palette colors to the shapes.

Some data labels intersect with other labels in this output. The following options are used to avoid intersecting:

## Smart labels

The Maps component provides an option to specify the smart labels when the labels intersect with the corresponding shape borders. In the `smartLabelMode` property, you can specify any of the following options:

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
                smartLabelMode: 'Hide'
            };
   }
}

```

{% endtab %}

## Intersect action

This specifies the intersect action when a label intersect with another label. In the `intersectionAction` property, you can specify any of the following options:

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