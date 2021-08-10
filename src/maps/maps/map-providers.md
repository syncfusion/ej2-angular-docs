---
title: " Maps providers in Angular Maps control | Syncfusion "

component: "Maps"

description: "Learn here all about Maps providers of Syncfusion Angular Maps control and more."
---

# Map Providers in Angular Maps control

Maps control support map providers such as OpenStreetMap that can be added to any layers in maps.

## Open Street Map

OpenStreetMap(OSM) is a online map provider. The OpenStreetMap allows you to view, edit and use geographical data in a collaborative way from any place on the Earth. One of the most important features in Maps control is the built-in online map provider support. By using this feature, you can render OpenStreetMaps in the maps component. This provides the ability to visualize street map tiles without using any external shape files.

``` typescript
import { Component, ViewEncapsulation } from '@angular/core';

@Component({
  selector: 'my-app',
  // specifies the template string for the maps component
  template:
    `><ejs-maps id='container'>
    <e-layers>
    <e-layer layerType='OSM' [urlTemplate]='urlTemplate'></e-layer>
    </e-layers>
  </ejs-maps`,
  encapsulation: ViewEncapsulation.None
})
export class AppComponent {
  public urlTemplate = 'http://a.tile.openstreetmap.org/level/tileX/tileY.png';
}

```

## Bing Maps

Bing Maps is a online map provider for accessing the external geospatial imagery services for deep-zoom satellite view which is supported in the Maps control. This provides the ability to visualize satellite, aerial, and street maps without using any external shape files.

```typescript
import { Component, ViewEncapsulation } from '@angular/core';

@Component({
  selector: 'my-app',
  // specifies the template string for the maps component
  template:
    `<ejs-maps id='container'>
    <e-layers>
    <e-layer layerType='Bing' bingMapType='AerialWithLabel' [key]='bingkey'></e-layer>
    </e-layers>
  </ejs-maps>`,
  encapsulation: ViewEncapsulation.None
})
export class AppComponent {
  public bingkey = "Your Bing Map Key";
}
```
