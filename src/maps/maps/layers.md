# Layers

Map is maintained through `layers` and it can accommodate one or more layers.

## Multilayer

The Multilayer support allows you to load multiple shape files in a single container, enabling maps to display more information.

### Adding Multiple Layers in the Map

The shape layers is the core layer of the map. The multiple layers can be added in the shape layer `type` as `SubLayer`.

## SubLayer

In this example, World Map shape is used as shape data by utilizing the `“WorldMap.json”`
file in the following folder structure obtained from downloaded Maps_GeoJSON folder.

..\ Maps_GeoJSON\

You can assign the complete contents in `WorldMap.json` file to new JSON object. For better understanding,
a TS file `WorldMap.ts` is already created to store JSON data in JSON object “world_map” and also copy the
USA.json file data, bind value to “usMap” like “world_map”.

`[WorldMap.ts]`

```typescript
export let world_map = //Paste all the content copied from the JSON file//
```

`[usa.ts]`

```typescript
export let usMap = //Paste all the content copied from the USA.JSON file//
```

**Note:** USA Map rendered as a sublayer using `layer.type` as "SubLayer".

[`app.component.ts`]

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps } from '@syncfusion/ej2-angular-maps';
import { usa_map } from 'usa.ts';
import { california } from 'california.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' [layers]='layers'>
     <e-layers>
    <e-layer [shapeData] = 'shapeData' [shapeSettings] ='shapeSettings'></e-layer>
    <e-layer [shapeData] = 'shapeData1' [shapeSettings] ='shapeSettings1' [type] = 'type'></e-layer>
    </e-layers>
    </ejs-maps>`
})
export class AppComponent implements OnInit {
    ngOnInit(): void {
           public shapeData: Object = usa_map;
           public shapeSettings: Object = {
                fill: '#E5E5E5',
                border: {
                    color: 'black',
                    width: 0.1
                }
            }
           public shapeData1: Object = california;
           public  type: String = 'SubLayer',
           public shapeSettings1: Object = {
                fill: 'rgba(141, 206, 255, 0.6)',
                border: {
                    color: '#1a9cff',
                    width: 0.25
                }
            }
    }
}

```

{% endtab %}

[`app.module.ts`]

```typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the MapsModule for the Maps component
import { MapsModule } from '@syncfusion/ej2-angular-maps';
import { AppComponent }  from './app.component';

@NgModule({
  // declaration of ej2-angular-maps module into NgModule
  imports:      [ BrowserModule, MapsModule ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

Refer the [`API`](../api/maps/layerSettingsModel) for Layers feature.

## Displaying layer in the view

In Maps, you can load multiple shape files. Using the `baseLayerIndex` property, you can select a layer to display on user interface.

In this example, we have two layers with the World map and the United States map share data and selected a layer using the `baseLayerIndex` property to show that layer on the web page.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps } from '@syncfusion/ej2-angular-maps';
import { usa_map } from 'usa.ts';
import { world_map } from 'world-map.ts';
import { california } from 'california.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' [baseLayerIndex] ='baseLayerIndex' [layers]='layers'>
     <e-layers>
    <e-layer [shapeData] = 'shapeData'></e-layer>
    <e-layer [shapeData] = 'shapeData1'></e-layer>
    </e-layers>
    </ejs-maps>`
})
export class AppComponent implements OnInit {
    ngOnInit(): void {
           public shapeData: Object = world_map;
           public shapeData1: Object = usa_map;
           public baseLayerIndex: number = 1;
    }
}

```

{% endtab %}

If you set the `baseLayerIndex` value to 0, the world map will be loaded.

This concept is used in the Maps drill-down feature, so the corresponding shape will be loaded when clicking a shape of the maps.

Refer the [`API`](../api/maps/layerSettingsModel/) for Layers feature.