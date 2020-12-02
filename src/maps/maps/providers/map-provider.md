# OpenStreetMap

The OpenStreetMap (OSM) is the world map built by a community of developers; it is free to use under an open license. It allows you to view geographical data in a collaborative way from anywhere on the earth. The OSM map provides small tile images to display the map area in the Maps component.

## Add OpenStreetMap

One of the most important features in EJ2 Maps component is the built-in online map provider support. By using this feature, you can render OpenStreetMap in the maps component. This provides the ability to visualize street map tiles without using any external shape files.

You can enable this feature by setting the value of `layerType` property to `OSM`

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
    `<ejs-maps id='rn-container' [layers]='layers'>
     <e-layers>
    <e-layer [layerType] = 'layerType'></e-layer>
    </e-layers>
    </ejs-maps>`
})
export class AppComponent implements OnInit {
    ngOnInit(): void {
           public layerType: string = 'OSM';
    }
}

```

{% endtab %}

## Zooming and panning

You can zoom and pan the OSM maps layer. Zooming helps you get a closer look at a particular area on a map for in-depth analysis. Panning helps you to move a map around to focus the targeted area.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

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
           public layerType: string = 'OSM';
           public zoomSettings: object = {
               enable: true
           }
    }
}

```

{% endtab %}

## Adding markers and navigation line

Markers can be added to the layers of OSM maps by setting the corresponding location's coordinates of latitude and longitude using `markerSettings` property. You can add navigation lines on top of an OSM maps layer for highlighting a path among various places by setting the corresponding location's coordinates of latitude and longitude in the `navigationLineSettings` property.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

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
    <e-layer [layerType] = 'layerType' [markerSettings]='markerSettings' [navigationLineSettings]='navigationLineSettings'></e-layer>
    </e-layers>
    </ejs-maps>`
})
export class AppComponent implements OnInit {
    ngOnInit(): void {
           public layerType: string = 'OSM';
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

{% endtab %}

## Sublayer

You can render any GeoJSON shape as a sublayer on top of an OSM maps layer for highlighting a particular continent or country in OSM maps by adding another layer and specifying the type to Sublayer

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
    `<ejs-maps id='rn-container' [layers]='layers'>
     <e-layers>
    <e-layer [layerType] = 'layerType'></e-layer>
    <e-layer [type] = 'type' [shapeData]='shapeData' [shapeSettings]='shapeSettings'></e-layer>
    </e-layers>
    </ejs-maps>`
})
export class AppComponent implements OnInit {
    ngOnInit(): void {
           public layerType: string = 'OSM';
           public type: string = 'SubLayer';
           public shapeData: object = usa_map;
           public shapeSettings: object = {
               fill: 'blue'
           };
    }
}

```

{% endtab %}