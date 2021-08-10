---
title: " Open Street Maps in Angular Maps control | Syncfusion "

component: "Maps"

description: "Learn here all about Open Street Maps of Syncfusion Angular Maps control and more."
---

# Open Street Maps in Angular Maps control

The OpenStreetMap (OSM) is the online map provider built by a community of developers; it is free to use under an open license. It allows to view geographical data in a collaborative way from anywhere on the earth. The OSM map provides small tile images based on our requests and combines those images into a single image to display the map area in the Maps component.

## Adding OpenStreetMap

The OSM map can be rendered using by setting the [`layerType`](../api/maps/layerSettingsModel/#layertype) property value as "**OSM**".

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

### Changing the tile server of the OpenStreetMap

The OSM tile server can be changed by setting the tile URL in the [`urlTemplate`](../api/maps/layerSettingsModel/#urltemplate) property. For more details about the OSM tile server, refer [here](https://wiki.openstreetmap.org/wiki/Tiles).

{% endtab %}

## Zooming and panning

The OSM maps layer can be zoomed and panned. Zooming helps to get a closer look at a particular area on a map for in-depth analysis. Panning helps to move a map around to focus the targeted area.

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

Markers can be added to the layers of OSM maps by setting the corresponding location's coordinates of latitude and longitude using [`markerSettings`](../api/maps/layerSettingsModel/#markersettings) property. Navigation lines can be added on top of an OSM maps layer for highlighting a path among various places by setting the corresponding location's coordinates of latitude and longitude in the [`navigationLineSettings`](../api/maps/layerSettingsModel/#navigationlinesettings) property.

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

Any GeoJSON shape can be rendered as a sublayer on top of the OSM maps layer for highlighting a particular continent or country in OSM maps by adding another layer and specifying the [`type`](../api/maps/layerSettingsModel/#type) property of maps layer to "**SubLayer**".

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