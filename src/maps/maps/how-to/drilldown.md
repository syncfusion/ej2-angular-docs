# Drilldown

By clicking a continent, you can view all the countries available in that continent using the drill-down
feature. For example, the countries in the `Africa` continent have been showcased here. You can showcase
all the countries in `Africa` continent by clicking the [shapeSelected](../../api/maps/#shapeselected)
event as mentioned in the following code example.

[`app.module.ts`]

```typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent }  from './app.component';
import { MapsModule } from '@syncfusion/ej2-angular-maps';
import { HighlightService,MarkerService } from '@syncfusion/ej2-angular-maps';


@NgModule({
  imports:      [ BrowserModule,MapsModule ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ],
  providers:    [ HighlightService,MarkerService ]
})
export class AppModule { }
```

[`app.component.ts`]

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
    </div>`,
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
    //    fill: 'blue'
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
    public africa_shapeSettings={
        fill: '#80306A'
    };
    public highlightSettings={
        enable: true,
        fill: '#80306A'
    };
}
```

```html
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
       </style>
```