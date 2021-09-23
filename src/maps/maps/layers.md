---
title: " Layers in Angular Maps control | Syncfusion "

component: "Maps"

description: "Learn here all about Layers feature of Syncfusion Angular Maps control and more."
---

# Layers in Angular Maps control

The Maps control is rendered through [`layers`](../api/maps/#layers) and any number of layers can be added to the Maps.

## Multilayer

The Multilayer support allows loading multiple shape files and map providers in a single container, enabling Maps to display more information. The shape layer or map providers are the main layers of the Maps. Multiple layers can be added as **SubLayer** over the main layers using the [`type`](../api/maps/layerSettingsModel/#type) property of [`layers`](../api/maps/#layers).

## Sublayer

Sublayer is a type of shape file layer. It allows loading multiple shape files in a single map view. For example, a sublayer can be added over the main layer to view geographic features such as rivers, valleys and cities in a map of a country. Similar to the main layer, elements in the Maps such as markers, bubbles, color mapping and legends can be added to the sub-layer.

In this example, the United States map shape is used as shape data by utilizing **usa.ts** file, and **texas.ts** and **california.ts** files are used as sub-layers in the United States map.

[`app.component.ts`]

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { Maps } from '@syncfusion/ej2-angular-maps';
import { usa_map } from 'usa.ts';
import { california } from 'california.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container'>
     <e-layers>
    <e-layer [shapeData] = 'shapeData' [shapeSettings] ='shapeSettings'></e-layer>
    <e-layer [shapeData] = 'shapeData1' [shapeSettings] ='shapeSettings1' [type] = 'type'></e-layer>
    </e-layers>
    </ejs-maps>`
})
export class AppComponent implements OnInit {
    public shapeData: object;
    public shapeSettings: object;
    public shapeData1: object;
    public  type: string;
    public shapeSettings1: object;
    ngOnInit(): void {
        this.shapeData = usa_map;
        this.shapeSettings = {
            fill: '#E5E5E5',
            border: {
                color: 'black',
                width: 0.1
            }
        }
        this.shapeData1 = california;
        this.type = 'SubLayer',
        this.shapeSettings1 = {
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

## Displaying different layer in the view

Multiple shape files and map providers can be loaded simultaneously in Maps. The [`baseLayerIndex`](../api/maps/mapsModel/#baselayerindex) property is used to determine which layer on the user interface should be displayed. This property is used for the Maps drill-down feature, so when the [`baseLayerIndex`](../api/maps/mapsModel/#baselayerindex) value is changed, the corresponding shape is loaded. In this example, two layers can be loaded with the World map and the United States map. Based on the given [`baseLayerIndex`](../api/maps/mapsModel/#baselayerindex) value the corresponding shape will be loaded in the user interface. If the [`baseLayerIndex`](../api/maps/mapsModel/#baselayerindex) value is set to **0**, then the world map will be loaded.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { Maps } from '@syncfusion/ej2-angular-maps';
import { usa_map } from 'usa.ts';
import { world_map } from 'world-map.ts';
import { california } from 'california.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' [baseLayerIndex] ='baseLayerIndex'>
     <e-layers>
    <e-layer [shapeData] = 'shapeData'></e-layer>
    <e-layer [shapeData] = 'shapeData1'></e-layer>
    </e-layers>
    </ejs-maps>`
})
export class AppComponent implements OnInit {
    public shapeData: object;
    public shapeData1: object;
    public baseLayerIndex: number;
    ngOnInit(): void {
        this.shapeData = world_map;
        this.shapeData1 = usa_map;
        this.baseLayerIndex = 1;
    }
}

```

{% endtab %}