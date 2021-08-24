# Display geometry shape in bing maps

Usually bing map displays the Maps in satellite view in which you can't make changes as per your requirement. To over come this, you can add maps shape as sublayer over the bing map and you can customize it as per your requirement. Kindly follow the below steps to add geometry shapes as sublayer in bing maps.

**Step 1**:

To render the Maps control as bing map, set the [`layerType`](../api/maps/layerSettingsModel/#layertype) as **Bing** and also provide the key for the bing map.

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
    public layerType: string;
    public key: string;
    ngOnInit(): void {
        this.layerType = "Bing";
        this.key= "../bingmapkey"
    }
}
```

**Step 2**:

The geometry shape can be added in the bing map using sublayer concept. In the below example, Africa continent can be set as the sublayer in bing map using the [`type`](../api/maps/layerSettingsModel/#type) property.

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
    public layerType: string;
    public key: string;
    public shapeData: object;
    public shapeSettings: object;
    ngOnInit(): void {
        this.layerType = "Bing";
        this.key= "../bingmapkey";
        this.shapeData = africa_continent;
        this.shapeSettings = {
            fill: 'blue'
        }
    }
}
```