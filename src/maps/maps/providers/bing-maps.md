---
title: "Bing Maps in Angular Maps control | Syncfusion"

component: "Maps"

description: "Learn here all about Bing Maps of Syncfusion Angular Maps control and more."
---

# Bing Maps in Angular Maps control

Bing Maps is a online Maps provider, owned by Microsoft. As like OSM, it provide Maps tile images based on our requests and combines those images into a single one to display Maps area.

## Adding Bing Maps

The Bing Maps can be rendered by setting the [`layerType`](../api/maps/layerSettingsModel/#layertype) property as **Bing** and the key for the Bing Maps must be set in the [`key`](../api/maps/layerSettingsModel/#key) property. The Bing Maps key can be obtained from [here](https://www.microsoft.com/en-us/maps/create-a-bing-maps-key).

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' style="display:block">
     <e-layers>
    <e-layer [layerType] = 'layerType' [bingMapType] = 'bingMapType' [key]='key'></e-layer>
    </e-layers>
    </ejs-maps>`
})
export class AppComponent implements OnInit {
    public layerType: string;
    public bingMapType: string;
     public key: string;
    ngOnInit(): void {
           this.layerType = 'Bing';
           this.bingMapType = 'AerialWithLabel';
           this.key = '//..bingmapkey';
    }
}

```

>Specify Bing Maps key in the `key` property.

## Types of Bing Maps

Bing Maps provides different types of Maps and it is supported in the Maps control.

* **Aerial** - Displays satellite images to highlight roads and major landmarks for easy identification.
* **AerialWithLabel** - Displays aerial Maps with labels for the continent, country, ocean, etc.
* **Road** - Displays the default Maps view of roads, buildings, and geography.
* **CanvasDark** - Displays dark version of the road Maps.
* **CanvasLight** - Displays light version of the road Maps.
* **CanvasGray** - Displays grayscale version of the road Maps.

To render the light version of the road Maps, set the `bingMapType` to `CanvasLight` as demonstrated in the following code sample.

```typescript

import { Component, OnInit} from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' style="display:block">
     <e-layers>
    <e-layer [layerType] = 'layerType' [bingMapType] = 'bingMapType' [key]='key'></e-layer>
    </e-layers>
    </ejs-maps>`
})
export class AppComponent implements OnInit {
    public layerType: string;
    public bingMapType: string;
    public key: string;
    ngOnInit(): void {
           this.layerType = 'Bing';
           this.bingMapType = 'CanvasLight';
           this.key = '//..bingmapkey';
    }
}

```

>Specify Bing Maps key in the `key` property.

## Zooming and Panning

Bing Maps layer can be zoomed and panned. Zooming helps to get a closer look at a particular area on a Maps for in-depth analysis. Panning helps to move a Maps around to focus the targeted area.

```typescript

import { Component, OnInit } from '@angular/core';
import { Maps, Zoom } from '@syncfusion/ej2-angular-maps';
Maps.Inject(Zoom);
@Component({
  selector: 'app-container',
  template: `
    <ejs-maps id="rn-container" [zoomSettings]="zoomSettings" style="display:block">
      <e-layers>
        <e-layer [layerType]="layerType" [key]="key" [bingMapType]="bingMapType"></e-layer>
      </e-layers>
    </ejs-maps>
  `
})
export class AppComponent implements OnInit {
  public layerType: string;
  public zoomSettings: object;
  public bingMapType: string;
  public key: string;
  ngOnInit(): void {
    this.layerType = 'Bing';
    this.bingMapType = 'CanvasLight';
    this.key = '//..bingmapkey';
    this.zoomSettings = {
      enable: true
    };
  }
}

```

>Specify Bing Maps key in the `key` property.

## Adding markers and navigation line

Markers can be added to the layers of Bing Maps by setting the corresponding location's coordinates of latitude and longitude using [`markerSettings`](../api/maps/layerSettingsModel/#markersettings). Navigation lines can be added on top of an Bing Maps layer for highlighting a path among various places by setting the corresponding location's coordinates of latitude and longitude in the [`navigationLineSettings`](../api/maps/layerSettingsModel/#navigationlinesettings).

```typescript

import { Component, OnInit } from '@angular/core';
import { Maps, Zoom, Marker, NavigationLine } from '@syncfusion/ej2-angular-maps';

Maps.Inject(Zoom, Marker, NavigationLine);
@Component({
  selector: 'app-container',
  template: `
    <ejs-maps id="rn-container" style="display:block" [zoomSettings]="zoomSettings" [centerPosition]="centerPosition">
      <e-layers>
        <e-layer [layerType]="layerType" [bingMapType]="bingMapType" [key]="key" [markerSettings]="markerSettings" [navigationLineSettings]="navigationLineSettings"></e-layer>
      </e-layers>
    </ejs-maps>
  `
})
export class AppComponent implements OnInit {
  public layerType: string;
  public bingMapType: string;
  public key: string;
  public zoomSettings: object;
  public centerPosition: object;
  public markerSettings: object;
  public navigationLineSettings: object;
  ngOnInit(): void {
    this.layerType = 'Bing';
    this.bingMapType = 'CanvasLight';
    this.key = '//..bingmapkey';
    this.zoomSettings = {
      zoomFactor: 4
    };
    this.centerPosition = {
      latitude: 29.394708,
      longitude: -94.954653
    };
    this.markerSettings = [
      {
        visible: true,
        height: 25,
        width: 15,
        dataSource: [
          {
            latitude: 34.06062,
            longitude: -118.330491,
            name: 'California'
          },
          {
            latitude: 40.724546,
            longitude: -73.850344,
            name: 'New York'
          }
        ]
      }
    ];
    this.navigationLineSettings = [
    {
        visible: true,
        color: 'blue',
        width: 5,
        angle: 0.1,
        latitude: [34.06062, 40.724546],
        longitude: [-118.330491, -73.850344]
    }];
  }
}

```

>Specify Bing Maps key in the `Key` property.

## Sublayer

Any GeoJSON shape can be rendered as a sublayer on top of the Bing Maps layer for highlighting a particular continent or country in Bing Maps by adding another layer and specifying the [`type`](../api/maps/layerSettingsModel/#type) property of Maps layer to **SubLayer**.