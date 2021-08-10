# Drilldown

By clicking a continent, all the countries available in that continent can be viewed using the drill-down feature. For example, the countries in the `Africa` continent have been showcased here. To showcase all the countries in `Africa` continent by clicking the [`shapeSelected`](../api/maps#shapeselected) event as mentioned in the following example.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation,ViewChild } from '@angular/core';
import { IShapeSelectedEventArgs, MapsComponent} from '@syncfusion/ej2-angular-maps';
import { World_Map } from './MapData/WorldMap';
import { Africa } from './MapData/Africa';
import { dafaultData } from './MapData/salesCountry';
export interface ShapeData { continent?: string; }

@Component({
    selector: 'my-app',
    // specifies the template string for the maps component
    template:`<div class="control-section">
    <div align='center'>
    <ejs-maps id='container' #drilldown (shapeSelected)="shapeSelected($event)" style="display:block;">
    <e-layers>
    <e-layer [shapeData]='worldmap' layerType='Geometry' shapePropertyPath='continent' shapeDataPath='continent' [dataSource]='dataSource' [shapeSettings]='shapeSettings' [markerSettings]='markerSettings'></e-layer>
    <e-layer layerType='Geometry' [shapeData]='africa' [shapeSettings]='africa_shapeSettings' [highlightSettings]='highlightSettings'></e-layer>
    </e-layers>
    </ejs-maps>
    </div>
    </div>
    <style>
        .markerTemplate {
            font-size: 12px;
            color: white;
            text-shadow: 0px 1px 1px black;
            font-weight: 500
        }
        .markerTemplate {
            height: 30px;
            width: 30px;
            display: block;
            margin: auto;
        }
       </style>`,
    encapsulation: ViewEncapsulation.None
  })

export class AppComponent {
    public worldmap=World_Map;
    public dataSource=dafaultData;
    public africa=Africa;
    @ViewChild('drilldown')
    public maps: MapsComponent;
    public shapeSelected = (args: IShapeSelectedEventArgs) : void => {
        let shape: string = (args.shapeData as ShapeData).continent;
        if (shape === 'Africa') {
            this.maps.baseLayerIndex=1;
            this.maps.refresh();
        }
    };
    public shapeSettings = {
        colorValuePath: 'drillColor'
    };
    public markerSettings=[{
        visible: true,
        template: '<div id="marker3" class="markerTemplate">Africa' +
            '</div>',
        dataSource: [
            { latitude: 10.97274101999902, longitude: 16.390625 }
        ],
        animationDuration: 0
    }];
    public africa_shapeSettings = {
        fill: '#80306A'
    };
    public highlightSettings = {
        enable: true,
        fill: '#80306A'
    };
}
```

{% endtab %}