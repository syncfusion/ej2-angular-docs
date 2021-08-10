# Display geometry shape in bing maps

Usually bing map displays the Maps in satellite view in which you can't make changes as per your requirement. To over come this, you can add maps shape as sublayer over the bing map and you can customize it as per your requirement. Kindly follow the below steps to add geometry shapes as sublayer in bing maps.

**Step 1**:

To render the Maps control as bing map, set the [`layerType`](../api/maps/layerSettingsModel/#layertype) as **Bing** and also provide the key for the bing map.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps } from '@syncfusion/ej2-angular-maps';

@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container'>
    <e-layers>
    <e-layer  [layerType]= 'layerType' [key] = 'key'></e-layer>
    </e-layers>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    ngOnInit(): void {
        public layerType = "Bing";
        public key= "AuQazZ3PUo3p2_c2KPhqMku-iKvee5fKcRREIg46MENqVTM9dp2ZyTbrHJpR9esZ"
    }
}
```

 {% endtab %}

**Step 2**:

The geometry shape can be added in the bing map using sublayer concept. In the below example, Africa continent can be set as the sublayer in bing map using the [`type`](../api/maps/layerSettingsModel/#type) property.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps } from '@syncfusion/ej2-angular-maps';
import { africa_continent } from 'africa-continent.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container'>
    <e-layers>
    <e-layer [layerType]= 'layerType' [key] ='key'></e-layer>
     <e-layer [shapeData]= 'shapeData' [type] ='Sublayer' [shapeSettings]='shapeSettings'></e-layer>
    </e-layers>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    ngOnInit(): void {
        public layerType = "Bing";
        public key= "AuQazZ3PUo3p2_c2KPhqMku-iKvee5fKcRREIg46MENqVTM9dp2ZyTbrHJpR9esZ";
        public shapeData: Object = africa_continent;
        public shapeSettings: Object = {
            fill: 'blue'
        }
    }
}
```

 {% endtab %}