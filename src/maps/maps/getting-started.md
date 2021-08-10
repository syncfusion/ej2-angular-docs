# Getting Started

This section explains you the steps required to create a map and demonstrate the basic usage of the maps control.

You can explore some useful features in the Maps component using the following video.

`youtube:kwE6ikF7QYQ`

## Setup Angular Environment

You can use [`Angular CLI`](https://github.com/angular/angular-cli) to setup your Angular applications.
To install Angular CLI use the following command.

```bash
npm install -g @angular/cli
```

## Create an Angular Application

Start a new Angular application using below Angular CLI command.

```bash
ng new my-app
cd my-app
```

## Adding Syncfusion Maps package

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) registry.

To install maps component, use the following command.

```bash
npm install @syncfusion/ej2-angular-maps --save
```

> The **--save** will instruct NPM to include the maps package inside of the `dependencies` section of the `package.json`.

## Registering Maps Module

Import Maps module into Angular application(app.module.ts) from the package `@syncfusion/ej2-angular-maps` [src/app/app.module.ts].

```typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the MapsModule for the Maps component
import { MapsModule } from '@syncfusion/ej2-angular-maps';
import { AppComponent }  from './app.component';

@NgModule({
  //declaration of chart module into NgModule
  imports:      [ BrowserModule, MapsModule ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

* Modify the template in `app.component.ts` file to render the `ej2-angular-maps` component
`[src/app/app.component.ts]`.

```javascript
import { Component, ViewEncapsulation } from '@angular/core';

@Component({
  selector: 'app-container',
  // specifies the template string for the maps component
  template: `<ejs-maps id='maps-container'></ejs-maps>`,
  encapsulation: ViewEncapsulation.None
})
export class AppComponent  { }
```

<!-- markdownlint-disable MD033 -->

Now use the <code>app-container</code> in the index.html instead of default one.

```html
<app-container></app-container>
```

* Now run the application in the browser using the below command.

```cmd
npm start
```

The below example shows a basic map.

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    // specifies the template string for the maps component
    template: `<ejs-maps id="maps-container"></ejs-maps>`
})
export class AppComponent {

}
```

As we didn't specify shapeData to the maps, no shape will be rendered and only an empty SVG element is appended to the maps container.

## Module Injection

Maps component are segregated into individual feature-wise modules. In order to use a particular feature,
you need to inject its feature module using `Maps.Inject()` method.  Find the modules available in maps and its description as follows.

* `AnnotationsService` - Inject this provider to use annotations feature.
* `BubbleService` - Inject this provider to use bubble feature.
* `DataLabelService` - Inject this provider to use data label feature.
* `HighlightService` - Inject this provider to use highlight feature.
* `LegendService` - Inject this provider to use legend feature.
* `MarkerService` - Inject this provider to use marker feature.
* `MapsTooltipService` - Inject this provider to use tooltip series.
* `NavigationLineService` - Inject this provider to use navigation lines feature.
* `SelectionService` - Inject this provider to use selection feature.
* `ZoomService` - Inject this provider to use zooming and panning feature.

For this application we are going to use tooltip, data label and legend features of the maps.
Now import the MapsTooltip, DataLabel and Legend modules from maps package
`@syncfusion/ej2-angular-maps`

 ```javascript
    import { NgModule } from '@angular/core';
    import { BrowserModule } from '@angular/platform-browser';
    import { AppComponent } from './app.component';
    import { MapsComponent,LegendService, DataLabelService,MapsTooltipService} from '@syncfusion/ej2-angular-maps';

    @NgModule({
        imports: [
            BrowserModule,
        ],
        declarations: [AppComponent, MapsComponent],
        bootstrap: [AppComponent],
        providers: [ MapsComponent,LegendService, DataLabelService,MapsTooltipService ]
    })

```

## Render shapes from GeoJSON data

This section explains how to bind GeoJSON data to the map.

```javascript

let usMap: Object =
{
    "type": "FeatureCollection",
    "crs": { "type": "name", "properties": { "name": "urn:ogc:def:crs:OGC:1.3:CRS84" } },
    "features": [
        { "type": "Feature", "properties": { "iso_3166_2": "MA", "name": "Massachusetts", "admin": "United States of America" }, "geometry":{
            "type": "MultiPolygon",
            "coordinates": [ [ [ [ -70.801756294617277, 41.248076234530558 ]] ] ] }
        }
    ]
    //..
};

```

Elements in the maps will get rendered in the layers. So add a layer collection to the maps by using [`layers`]property. Now bind the GeoJSON data to the [`shapeData`] property.

[`app.module.ts`]

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container'>
     <e-layers>
    <e-layer [shapeData] = 'shapeData'></e-layer>
    </e-layers>
    </ejs-maps>`
})
export class AppComponent implements OnInit {
    ngOnInit(): void {
           public shapeData: object = world_map;
    }
}
```

{% endtab %}

<!-- markdownlint-disable MD022 -->
## Bind data source to map
<!-- markdownlint-disable MD009 -->
The following properties in layers are used for binding data source to map.

* dataSource
* shapeDataPath
* shapePropertyPath

The [`dataSource`](../api/maps/layerSettingsModel/#datasource) property takes collection value as input. For example, the list of objects can be provided as input. This data is further used in tooltip, data label, bubble, legend and in color mapping.

The [`shapeDataPath`](../api/maps/layerSettingsModel/#shapedatapath) property used to refer the data ID in dataSource. Where as, the [`shapePropertyPath`](../api/maps/layerSettingsModel/#shapepropertypath) property is used to refer the column name in shapeData to identify the shape. Both the properties are related to each other. When the values of the shapeDataPath property in the dataSource property and the value of shapePropertyPath in the shapeData property match, then the associated object from the dataSource is bound to the corresponding shape.

The JSON object "electionData" is used as data source below.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' >
    <e-layers>
    <e-layer  [shapeData]= 'shapeData'  [shapePropertyPath]= 'shapePropertyPath' [shapeDataPath]= 'shapeDataPath' [dataSource] = 'dataSource'></e-layer>
    </e-layers>
    </ejs-maps>`
})
export class AppComponent implements OnInit {
    ngOnInit(): void {
        public dataSource: Object[] = [{  "Country": "China", "Membership": "Permanent"},
            {"Country": "France","Membership": "Permanent" },
            { "Country": "Russia","Membership": "Permanent"},
            {"Country": "Kazakhstan","Membership": "Non-Permanent"},
            { "Country": "Poland","Membership": "Non-Permanent"},
            {"Country": "Sweden","Membership": "Non-Permanent"}];
            public shapeData: Object = world_map;
    public shapePropertyPath: String = 'name';
    public shapeDataPath: String= 'Country';
    };
}

```

{% endtab %}

## Apply Color Mapping

The Color Mapping feature supports customization of shape colors based on the underlying value of shape received from bounded data. Specify the field name from which the values have to be compared for the shapes in [`colorValuePath`](../api/maps/shapeSettingsModel/#colorvaluepath) property in [`shapeSettings`](../api/maps/shapeSettingsModel/).

Specify color and value in [`colorMapping`](../api/maps/shapeSettingsModel/#colormapping) property. Here '#D84444' is specified for 'Trump' and '#316DB5' is specified for 'Clinton'.

[`app.module.ts`]

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' >
    <e-layers>
    <e-layer  [shapeData]= 'shapeData'  [shapePropertyPath]= 'shapePropertyPath' [shapeDataPath]= 'shapeDataPath' [dataSource] = 'dataSource' [shapeSettings] = 'shapeSettings'></e-layer>
    </e-layers>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    ngOnInit(): void {
            public dataSource: Object[] = [{  "Country": "China", "Membership": "Permanent"},
            {"Country": "France","Membership": "Permanent" },
            { "Country": "Russia","Membership": "Permanent"},
            {"Country": "Kazakhstan","Membership": "Non-Permanent"},
            { "Country": "Poland","Membership": "Non-Permanent"},
            {"Country": "Sweden","Membership": "Non-Permanent"}];
            public shapeData: Object = world_map;
    public shapePropertyPath: String = 'name';
    public shapeDataPath: String= 'Country';
    public shapeSettings: Object = {
                colorValuePath: 'Membership',
                colorMapping: [
                {
                    value: 'Permanent', color: '#D84444'
                },
                {
                    value: 'Non-Permanent', color: '#316DB5'
                }]
            };
   }
}

```

{% endtab %}

## Add Title for Maps

You can add a title using [`titleSettings`](../api/maps/titleSettingsModel/) property to the map to provide quick
information to the user about the shapes rendered in the map.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' [titleSettings] = 'titleSettings' >
    <e-layers>
    <e-layer  [shapeData]= 'shapeData'  [shapePropertyPath]= 'shapePropertyPath' [shapeDataPath]= 'shapeDataPath' [dataSource] = 'dataSource' [shapeSettings] = 'shapeSettings'></e-layer>
    </e-layers>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    ngOnInit(): void {
        public titleSettings: object = {
         text: 'World map membership',
          titleStyle: {
            size: '16px'
           }
        }
            public dataSource: Object[] = [{  "Country": "China", "Membership": "Permanent"},
            {"Country": "France","Membership": "Permanent" },
            { "Country": "Russia","Membership": "Permanent"},
            {"Country": "Kazakhstan","Membership": "Non-Permanent"},
            { "Country": "Poland","Membership": "Non-Permanent"},
            {"Country": "Sweden","Membership": "Non-Permanent"}];
            public shapeData: Object = world_map;
    public shapePropertyPath: String = 'name';
    public shapeDataPath: String= 'Country';
    public shapeSettings: Object = {
                colorValuePath: 'Membership',
                colorMapping: [
                {
                    value: 'Permanent', color: '#D84444'
                },
                {
                    value: 'Non-Permanent', color: '#316DB5'
                }]
            };
   }
}

```

{% endtab %}

## Enable Legend

You can show legend for the maps by setting true to the [`visible`](../api/maps/legendSettingsModel/#visible)
property in [`legendSettings`](../api/maps/legendSettingsModel/) object and by injecting the `LegendService`
module using `@NgModule.providers` method.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps, Legend } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';

Maps.Inject(Legend);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' [legendSettings] = 'legendSettings'>
    <e-layers>
    <e-layer  [shapeData]= 'shapeData'  [shapePropertyPath]= 'shapePropertyPath' [shapeDataPath]= 'shapeDataPath' [dataSource] = 'dataSource' [shapeSettings] = 'shapeSettings'></e-layer>
    </e-layers>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    ngOnInit(): void {
            public dataSource: Object[] = [{  "Country": "China", "Membership": "Permanent"},
            {"Country": "France","Membership": "Permanent" },
            { "Country": "Russia","Membership": "Permanent"},
            {"Country": "Kazakhstan","Membership": "Non-Permanent"},
            { "Country": "Poland","Membership": "Non-Permanent"},
            {"Country": "Sweden","Membership": "Non-Permanent"}];
            public shapeData: Object = world_map;
    public shapePropertyPath: String = 'name';
    public shapeDataPath: String= 'Country';
    public shapeSettings: Object = {
                colorValuePath: 'Membership',
                colorMapping: [
                {
                    value: 'Permanent', color: '#D84444'
                },
                {
                    value: 'Non-Permanent', color: '#316DB5'
                }]
            };
            public legendSettings: Object = {
                visible: true
                }
   }
}

```

{% endtab %}

## Add Data Label

You can add data labels to show additional information of the shapes in map. This can be achieved by setting [`visible`](../api/maps/dataLabelSettingsModel/#visible) property to true in the [`dataLabelSettings`](../api/maps/dataLabelSettingsModel/) object and by injecting `DataLabelService` module using `@NgModule.providers` method.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps, DataLabel } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';

Maps.Inject(DataLabel);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container'  >
    <e-layers>
    <e-layer  [shapeData]= 'shapeData' [shapeSettings] = 'shapeSettings' [dataLabelSettings] = 'dataLabelSettings'></e-layer>
    </e-layers>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    ngOnInit(): void {
         public shapeData: Object = world_map;
         public shapeSettings: Object = {
                autofill: true
            };
            public dataLabelSettings: Object = {
                visible: true,
                labelPath: 'name',
                smartLabelMode: 'Trim'
            };
   }
}

```

{% endtab %}

## Enable Tooltip

The tooltip is useful when you cannot display information by using the data labels due to space constraints.
You can enable tooltip by setting the [`visible`](../api/maps/tooltipSettingsModel/#visible) property as true
in [`tooltipSettings`](../api/maps/tooltipSettingsModel/) object and by injecting `MapsTooltipService` module using
`@NgModule.providers` method.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps, MapsTooltip, DataLabel } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';

Maps.Inject(MapsTooltip, DataLabel);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container'  >
    <e-layers>
    <e-layer  [shapeData]= 'shapeData' [shapeSettings] = 'shapeSettings' [dataLabelSettings] = 'dataLabelSettings'[tooltipSettings] = 'tooltipSettings'></e-layer>
    </e-layers>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    ngOnInit(): void {
         public shapeData: Object = world_map;
         public shapeSettings: Object = {
                autofill: true
            };
            public dataLabelSettings: Object = {
                visible: true,
                labelPath: 'name',
                smartLabelMode: 'Trim'
            };
            public tooltipSettings: Object = {
                visible: true,
                valuePath: 'name'
            };
   }
}

```

{% endtab %}