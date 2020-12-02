# Markers

Markers are notes that are used to leave a message on the map. It indicates or marks a specific location with desired symbols on the maps.

The `dataSource` property has a list of objects that contains data for markers. By default, it displays the bound data at the specified latitude and longitude. Using the `visible` API, you can enable or disable the markers.
There are two ways to set marker for map.

* Marker and marker template

* Adding marker objects to map.

## Marker and marker template

The `markerSettings.dataSource` property has a list of objects that contains the data for Annotation.
By default, it displays the bound data at the specified latitude and longitude. The `markerSettings.template`
property is used for customizing the template for markers.

**Note:** markerSettings is an Array property.

[`app.component.ts`]

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps, Marker } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(Marker);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container'  >
    <e-layers>
    <e-layer  [shapeData]= 'shapeData' [markerSettings] = 'markerSettings'></e-layer>
    </e-layers>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    ngOnInit(): void {
         public shapeData: Object = world_map;
         public markerSettings: Object = [
                      {
                        visible: true,
                        template: '<div id="marker4" class="markerTemplate">Europe' +
                            '</div>',
                        dataSource: [
                            { latitude: 49.95121990866204, longitude: 18.468749999999998 }
                        ],
                        animationDuration: 0,
                    },
                    {
                        visible: true,
                        template: '<div id="marker5" class="markerTemplate" style="width:50px">North America' +
                            '</div>',
                        dataSource: [
                            { latitude: 59.88893689676585, longitude: -109.3359375 }
                        ],
                        animationDuration: 0
                    },
                    {
                        visible: true,
                        template: '<div id="marker6" class="markerTemplate" style="width:50px">South America' +
                            '</div>',
                        dataSource: [
                            { latitude: -6.64607562172573, longitude: -55.54687499999999 }
                        ],
                        animationDuration: 0
                    },
                    ]
   }
}
```

 {% endtab %}

[`app.module.ts`]
Injecting MarkerService into NgModule.

```typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the MapsModule for the Maps component
import { MapsModule, MarkerService } from '@syncfusion/ej2-angular-maps';
import { AppComponent }  from './app.component';

@NgModule({
  // declaration of ej2-angular-maps module into NgModule
  imports:      [ BrowserModule, MapsModule ],
  declarations: [ AppComponent ],
  providers: [MarkerService],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## Adding marker objects to map

The n number of markers can be added to shape layers with `markerSettings.dataSource` property. Each dataSource object contains the following list of properties.

* label - Text that displays some information about the annotation in text format.
* latitude - Latitude point determine the Y-axis position of annotation.
* longitude - Longitude point determine the X-axis position of annotation.

```typescript
import { Component, ViewEncapsulation } from '@angular/core';
import { usMap } from './MapData/USA';

@Component({
  selector: 'my-app',
  // specifies the template string for the maps component
  template:
    `<ejs-maps id='container' [legendSettings]="legendSettings">
    <e-layers>
    <e-layer [shapeData]='usmap' [markerSettings]='markerSettings'></e-layer>
    </e-layers>
  </ejs-maps>`,
  encapsulation: ViewEncapsulation.None
})
export class AppComponent {
  public usmap = usMap;
  public markerSettings = [
    {
      visible: true,
      template: '<div><div style="margin-left:8px;height:45px;width:120px;margin-top:-23px;">' +
      '<label style="color:black;margin-left:15px;font-weight:normal;">\{\{:city\}\}</label></div></div>',
      dataSource: [
        { latitude: 37.0000, longitude: -120.0000, city: 'California' },
        { latitude: 40.7127, longitude: -74.0059, city: 'New York' },
        { latitude: 42, longitude: -93, city: 'Iowa' }
      ]
    }
  ];
}
```

[`app.module.ts`]
Injecting MarkerService into NgModule.

```typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the MapsModule for the Maps component
import { MapsModule, MarkerService } from '@syncfusion/ej2-angular-maps';
import { AppComponent }  from './app.component';

@NgModule({
  // declaration of ej2-angular-maps module into NgModule
  imports:      [ BrowserModule, MapsModule ],
  declarations: [ AppComponent ],
  providers: [MarkerService],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## Customize marker shapes from data source

### Bind different colors and shapes to the marker from data source

The location on the map is marked by different marker shapes using `shapeValuePath` property in `markerSettings`. Based on the field name in the data source bind the value to the `shapeValuePath` property. Also, you can customize the marker shape color by binding the color value field name in the data source to the `colorValuePath` property in `markerSettings`.

A default marker object is represented by `balloon` shape. You can set various shapes to the marker object by using `shape` property in `markerSettings`. Also, you can change the shapes of the marker from the datasource.

The following shapes are used for the marker object.
* Circle
* Rectangle
* Balloon
* Cross
* Polyline
* Diamond
* Star
* Triangle
* HorizontalLine
* VerticalLine
* pentagon

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps, Marker } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(Marker);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' >
    <e-layers>
    <e-layer  [shapeData]= 'shapeData' [markerSettings] = 'markerSettings'></e-layer>
    </e-layers>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    ngOnInit(): void {
         public shapeData: Object = world_map;
         public markerSettings: Object = [
        {
            visible: true,
            shapeValuePath:'shape',
            colorValuePath:'color',
            dataSource: [
                { latitude: 49.95121990866204, longitude: 18.468749999999998, name:'Europe', color:'red', shape:'Triangle' },
                { latitude: 59.88893689676585, longitude: -109.3359375, name:'North America',
                color:'blue', shape:'Pentagon' },
                { latitude: -6.64607562172573, longitude: -55.54687499999999, name:'South America',
                color:'green', shape:'InvertedTriangle' }
            ],
        },
        ];
   }
}
```

 {% endtab %}

## Marker Zooming

The map is initially scaled to the center value based on the marker distance. This can be achieved by setting `shouldZoomInitially` property in `zoomSettings` as `true`.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps, Marker, Zoom } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(Marker, Zoom);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container'  [zoomSettings] ='zoomSettings'>
    <e-layers>
    <e-layer  [shapeData]= 'shapeData' [markerSettings] = 'markerSettings'></e-layer>
    </e-layers>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    ngOnInit(): void {
        public shapeData: Object = world_map;
        public markerSettings: Object = [
        {
            visible: true,
            dataSource: [
                { latitude: 49.95121990866204, longitude: 18.468749999999998, name:'Europe' },
                { latitude: 59.88893689676585, longitude: -109.3359375, name:'North America' },
                { latitude: -6.64607562172573, longitude: -55.54687499999999, name:'South America'}
            ],
        },
        ];
        public zoomSettings: Object = {
            enable: true,
            horizontalAlignment:'Near',
            shouldZoomInitially: true
    },
   }
}
```

 {% endtab %}

## Marker Cluster Expand

The cluster is formed by grouping an identical and non-identical marker from the surrounding area. By clicking on the cluster and setting `allowClusterExpand` property in `markerClusterSettings` as `true` to expand the identical markers. If you zoom in any of the locations of the cluster, the number on the cluster will decrease and the overlapping marker will be split into an individual marker on the map. When you zoom out, it will increase the marker count and then cluster it again.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps, Marker, Legend, Zoom } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(Marker, Legend, Zoom);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container'  [zoomSettings] ='zoomSettings'  >
    <e-layers>
    <e-layer  [shapeData]= 'shapeData' [markerSettings] = 'markerSettings' [markerClusterSettings] = 'markerClusterSettings'></e-layer>
    </e-layers>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    ngOnInit(): void {
        public shapeData: Object = world_map;
        public markerSettings: Object = [
                    {
                        visible: true,
                        dataSource: [
                            { latitude: 49.95121990866204, longitude: 18.468749999999998, name:'Europe' },
                            { latitude: 49.95121990866204, longitude: 18.468749999999998, name:'Europe' },
                            { latitude: 49.95121990866204, longitude: 18.468749999999998, name:'Europe' },
                            { latitude: 49.95121990866204, longitude: 18.468749999999998, name:'Europe' },
                            { latitude: 49.95121990866204, longitude: 18.468749999999998, name:'Europe' },
                            { latitude: 49.95121990866204, longitude: 18.468749999999998, name:'Europe' },
                            { latitude: 49.95121990866204, longitude: 18.468749999999998, name:'Europe' }
                            { latitude: 59.88893689676585, longitude: -109.3359375, name:'North America' },
                            { latitude: -6.64607562172573, longitude: -55.54687499999999, name:'South America'}
                        ]
                    },
        ];
        public zoomSettings: Object = {
            enable: true,
            mouseWheelZoom : true,
        },
        public markerClusterSettings: Object = {
            allowClustering: true,
            allowClusterExpand: true,
            shape: 'Circle',
            height: 40,
            width: 40,
            labelStyle : { color: 'white'},
        },
   }
}
```

 {% endtab %}

## Enable the Legend for map markers

Legend can be enabled for marker using `legendSettings.type` as **Markers** and legend visible as true,
need to inject Legend module to Maps using the `LegendService`. Refer the code snippet to enable the legend for the markers.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps, Marker, Legend } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(Marker, Legend);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container'  [legendSettings] ='legendSettings'  >
    <e-layers>
    <e-layer  [shapeData]= 'shapeData' [markerSettings] = 'markerSettings'></e-layer>
    </e-layers>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    ngOnInit(): void {
         public shapeData: Object = world_map;
         public markerSettings: Object = [
                    {
                        visible: true,
                        legendText: 'name',
                        dataSource: [
                            { latitude: 37.6276571, longitude: -122.4276688, name: 'San Bruno' },
                            { latitude: 33.5302186, longitude: -117.7418381, name: 'Laguna Niguel' },
                            { latitude: 40.7424509, longitude: -74.0081468, name: 'New York' }
                        ],
                        shape: 'Circle'
                    },
        ];
        public legendSettings: Object = {
        visible: true,
        type: 'Markers'
    },
   }
}
```

 {% endtab %}

[`app.module.ts`]
Injecting MarkerService and LegendService into NgModule.

```typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the MapsModule for the Maps component
import { MapsModule, MarkerService, LegendService } from '@syncfusion/ej2-angular-maps';
import { AppComponent }  from './app.component';

@NgModule({
  // declaration of ej2-angular-maps module into NgModule
  imports:      [ BrowserModule, MapsModule ],
  declarations: [ AppComponent ],
  providers: [MarkerService, LegendService],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## Marker Clustering

Maps provides support to hide and cluster marker when they overlap each other. The number on a cluster indicates how many overlapped markers it contains. If you zoom any of the cluster locations, the number on the cluster will decrease and you will begin to see the individual markers on the map. When zooming out, the overlapping marker will increase so that you can cluster it again and increase the count over the cluster.

Using the `markerClusterSettings.allowClustering` API, you can enable or disable this cluster support. The `markerClusterSettings` API also helps to customize clusters.

The `MarkerClusterRendering` event occurs when each cluster is rendered. You can also use this to customize the cluster. The `markerClusterClick` and `markerClusterMouseMove` events on mouse move and on clicking the cluster.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild, OnInit  } from '@angular/core';
import { Maps, Marker, MapsTooltip, Zoom } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
import { cluster } from 'marker-location.ts';
Maps.Inject(Marker, MapsTooltip, Zoom);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' [zoomSettings] = 'zoomSettings' [layers] = 'layers'>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    ngOnInit(): void {
         public zoomSettings: object = {
                    enable: true
          };
          public layers: object = [{
              shapeData: world_map,
              shapeSettings: { fill: '#C1DFF5' },
              markerClusterSettings: {
                allowClustering: true,
                shape: 'Circle',
                height: 40,
                width: 40,
                labelStyle: { color: 'white' },
              },
              markerSettings: [{
                dataSource: cluster,
                visible: true,
                animationDuration: 0,
                shape: 'Balloon',
                height: 20,
                width: 20,
                tooltipSettings: {
                    visible: true,
                    valuePath: 'area',
                }
          }]
        }];
   }
}
```

 {% endtab %}

Refer the [`API`](../api/maps/markerSettingsModel) for Marker feature.