# Bing Maps

Bing maps is a map of the entire World owned by Microsoft. As link OSM, it provides map title images based on our requests and combines those images into a single one to display the map area.

## Add Bing Maps

One of the most important features in Blazor Maps Component is the built-in online map provider support. By using this feature, you can render Bing maps in the maps component. This provides the ability to visualize satellite, aerial and street maps without using any external shape files.

you can enable this feature by setting `layerType` to `bing`.

```typescript

import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps } from '@syncfusion/ej2-angular-maps';
import { usa_map } from 'usa.ts';
import { world_map } from 'world-map.ts';
import { california } from 'california.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' [layers]='layers'>
     <e-layers>
    <e-layer [layerType] = 'layerType' [bingMapType] = 'bingMapType' [key]='key'></e-layer>
    </e-layers>
    </ejs-maps>`
})
export class AppComponent implements OnInit {
    ngOnInit(): void {
           public layerType: string = 'Bing';
           public bingMapType: string = 'AerialWithLabel';
           public key: string = '// …bingMapKey';
    }
}

```

> Specify Bing map key in the `key` property.

## Types of Bing maps

* **Aerial** - Displays satellite images to highlight roads and major landmarks for easy identification.
* **AerialWithLabel** - Displays aerial map with labels for the continent, country, ocean, etc.
* **Road** - Displays the default map view of roads, buildings, and geography.
* **CanvasDark** - Displays dark version of the road maps.
* **CanvasLight** - Displays light version of the road maps.
* **CanvasGray** - Displays grayscale version of the road maps.

To render the light version of the road maps, set the `bingMapType` to `CanvasLight` as demonstrated in the following code sample.

```typescript

import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps } from '@syncfusion/ej2-angular-maps';
import { usa_map } from 'usa.ts';
import { world_map } from 'world-map.ts';
import { california } from 'california.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' [layers]='layers'>
     <e-layers>
    <e-layer [layerType] = 'layerType' [bingMapType] = 'bingMapType' [key]='key'></e-layer>
    </e-layers>
    </ejs-maps>`
})
export class AppComponent implements OnInit {
    ngOnInit(): void {
           public layerType: string = 'Bing';
           public bingMapType: string = 'CanvasLight';
           public key: string = '// …bingMapKey';
    }
}

```

> Specify Bing maps key in the `key` property.

## Zooming and panning

You can zoom and pan the Bing maps layer. Zooming helps you get a closer look at a particular area on a map for in-depth analysis. Panning helps you to move a map around to focus the targeted area.

```typescript

import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps, Zoom } from '@syncfusion/ej2-angular-maps';
import { usa_map } from 'usa.ts';
import { world_map } from 'world-map.ts';
import { california } from 'california.ts';
Maps.Inject(Zoom);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' [layers]='layers' [zoomSettings]='zoomSettings'>
     <e-layers>
    <e-layer [layerType] = 'layerType'></e-layer>
    </e-layers>
    </ejs-maps>`
})
export class AppComponent implements OnInit {
    ngOnInit(): void {
           public layerType: string = 'Bing';
           public zoomSettings: object = {
               enable: true
           }
    }
}

```

> Specify Bing map key in the `key` property.

## Adding markers and navigation line

Markers can be added to the layers of Bing maps by setting the corresponding location's coordinates of latitude and longitude using `markerSettings` property. You can add navigation lines on top of an Bing maps layer for highlighting a path among various places by setting the corresponding locations's coordinates of latitude and longitude in the `navigationLineSettings` property.

```typescript

import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps, Zoom, Marker, NavigationLine } from '@syncfusion/ej2-angular-maps';
import { usa_map } from 'usa.ts';
import { world_map } from 'world-map.ts';
import { california } from 'california.ts';
Maps.Inject(Zoom, Marker, NavigationLine);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' [layers]='layers' [zoomSettings]='zoomSettings' [centerPosition]='centerPosition'>
     <e-layers>
    <e-layer [layerType] = 'layerType' [bingMapType]= 'bingMapType' [key]='key' [markerSettings]='markerSettings' [navigationLineSettings]='navigationLineSettings'></e-layer>
    </e-layers>
    </ejs-maps>`
})
export class AppComponent implements OnInit {
    ngOnInit(): void {
           public layerType: string = 'Bing';
           public bingMapType: string = 'CanvasLight';
           public key: string = '// …bingMapKey';
           public zoomSettings: object = {
               zoomFactor: 4
           };
           public centerPosition: object = {
               latitude: 29.394708,
                longitude: -94.954653
           };
            public markerSettings: object = [{
                visible: true,
                height: 25,
                width: 15,
                dataSource: [
                    {
                        latitude: 34.060620,
                        longitude: -118.330491,
                        name: "California"
                    },
                    {
                        latitude: 40.724546,
                        longitude: -73.850344,
                        name: "New York"
                    }
                ]
            }];
            public navigationLineSettings: object = [{
                visible: true,
                color: "blue",
                width: 5,
                angle: 0.1,
                latitude: [34.060620, 40.724546],
                longitude: [-118.330491,-73.850344]
            }];
    }
}

```

> Specify Bing map key in the `Key` property.

## Sublayer

You can render any GeoJSON shape as a sublayer on top of an Bing maps layer for highlighting a particular continent or country in Bing maps by adding another layer and specifying the type to SubLayer.

## Key

The Bing maps key is provided as input to this key property. The Bing Maps key can be obtained from [Bing Maps](http://www.microsoft.com/maps/create-a-bing-maps-key.aspx).