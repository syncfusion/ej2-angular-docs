---
title: " Populating data in Angular Maps control | Syncfusion "

component: "Maps"

description: "Learn here all about Populating data in Syncfusion Angular Maps control and more."
---

# Populate data in Angular Maps control

This section explains how to populate data inputs and provide it to the Maps component.

## Shape data

The shape data collection describes geographical shape information that is available in GeoJSON format. The Map shapes are rendered with this data. The custom shapes such as seat selection in bus, seat selection in a cricket stadium and more useful information can be also added as [`shapeData`](../api/maps/layerSettingsModel/#shapedata) in the layer of the Maps.

```typescript
export let usMap = // Paste all the content copied from the JSON file.
```

## Data source

The [`dataSource`](../api/maps/layerSettingsModel/#datasource) property is used to represent statistical data in the Maps component, and it accepts a collection of values as input. For example, a list of objects as input can be provided to the data source. This data source will be used to color the map, display data labels, and display tooltip, among other things.

The data source is populated with JSON data relative to shape data and stored as JSON object. In the below example, **populationData** can be used as data source in Maps.

```typescript
export let populationData: object[] = [
    {
        'code': 'AF',
        'value': 53,
        'name': 'Afghanistan',
        'population': 29863010,
        'density': 119
    },
    {
        'code': 'AL',
        'value': 117,
        'name': 'Albania',
        'population': 3195000,
        'density': 111
    },
    {
        'code': 'DZ',
        'value': 15,
        'name': 'Algeria',
        'population': 34895000,
        'density': 15
    },
    {
        'code': 'AO',
        'value': 15,
        'name': 'Angola',
        'population': 18498000,
        'density': 15
    },
    {
        'code': 'AR',
        'value': 15,
        'name': 'Argentina',
        'population': 40091359,
        'density': 14
    },
    {
        'code': 'AM',
        'value': 109,
        'name': 'Armenia',
        'population': 3230100,
        'density': 108
    }
];
```

## Data binding

The following properties in the [`layers`](../api/maps/layerSettingsModel/) are used for binding data in the Maps control. Both the properties are related to each other.

* shapePropertyPath
* shapeDataPath

### shapePropertyPath

The [`shapePropertyPath`](../api/maps/layerSettingsModel/#shapepropertypath) property is used to refer the field name in the [`shapeData`](../api/maps/layerSettingsModel/#shapedata) property of shape layers to identify the shape. When the values of [`shapeDataPath`](../api/maps/layerSettingsModel/#shapedatapath) property from the [`dataSource`](../api/maps/layerSettingsModel/#datasource) property and [`shapePropertyPath`](../api/maps/layerSettingsModel/#shapepropertypath) property from the [`shapeData`](../api/maps/layerSettingsModel/#shapedata) property match, then the associated object from the data source is bound to the corresponding shape.

> `world-map.ts` file contains following data and its field **"name"** value is used to map the corresponding shape with the provided data source.

```typescript
export let world_map: object = {
    "type": "Feature",
    "properties": {
        "admin": "Afghanistan",
        "name": "Afghanistan",
        "continent": "Asia"
    },
    "geometry": { "type": "Polygon", "coordinates": [[[61.21081709172573, ... },
...

```

### shapeDataPath

The [`shapeDataPath`](../api/maps/layerSettingsModel/#shapedatapath) property is similar to the [`shapePropertyPath`](../api/maps/layerSettingsModel/#shapepropertypath) property, but it refers to the field name in the [`dataSource`](../api/maps/layerSettingsModel/#datasource) property. For example, [populationData](#data-source) contains the **code**, **value**, **name**, **population** and **density** fields. Here, the **name** field is set to the shapeDataPath to map the corresponding value of field name in shape data.

In the below example, both "**name**" fields contain the same value as "**Afghanistan**", this value is matched in both shape data and data source, so that the details associated with "**Afghanistan**" will be mapped to the corresponding shape and used to color the corresponding shape, display data labels, display tooltips, and more.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { Maps } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' >
    <e-layers>
    <e-layer  [shapeData]= 'shapeData'  [shapePropertyPath]= 'shapePropertyPath' [shapeDataPath]= 'shapeDataPath' [dataSource] = 'dataSource' [shapeSettings]='shapeSettings'></e-layer>
    </e-layers>
    </ejs-maps>`
})
export class AppComponent implements OnInit {
    public dataSource: object[];
    public shapeData: object;
    public shapePropertyPath: string;
    public shapeDataPath: string;
    public shapeSettings: object;
    ngOnInit(): void {
        this.dataSource = [  
            {
                'code': 'AF',
                'value': 53,
                'name': 'Afghanistan',
                'population': 29863010,
                'density': 119,
                'color': '#DEEBAE'
            },
            {
                'code': 'AL',
                'value': 117,
                'name': 'Albania',
                'population': 3195000,
                'density': 111,
                'color': '#A4D6AD'
            },
            {
                'code': 'DZ',
                'value': 15,
                'name': 'Algeria',
                'population': 34895000,
                'density': 15,
                'color': '#37AFAB'
            },
            {
                'code': 'AO',
                'value': 15,
                'name': 'Angola',
                'population': 18498000,
                'density': 15,
                'color': '#547C84'
            },
            {
                'code': 'AR',
                'value': 15,
                'name': 'Argentina',
                'population': 40091359,
                'density': 14,
                'color': '#CEBF93'
            },
            {
                'code': 'AM',
                'value': 109,
                'name': 'Armenia',
                'population': 3230100,
                'density': 108,
                'color': '#a69d70'
            }
        ]
        this.shapeData = world_map;
        this.shapePropertyPath = 'name';
        this.shapeDataPath= 'name';
        this.shapeSettings = {
            colorValuePath: 'color',
            fill: '#E5E5E5'
        }
    };
}

```

{% endtab %}

<!-- markdownlint-disable MD010 -->

## Binding complex data source

Data from data source can be bind to the Maps in two different ways.

1. Bind the field name directly to the properties as [`shapeDataPath`](../api/maps/layerSettingsModel/#shapedatapath), [`colorValuePath`](../api/maps/markerSettingsModel/#colorvaluepath),
[`valuePath`](../api/maps/tooltipSettingsModel/#valuepath) and [`shapeValuePath`](../api/maps/markerSettingsModel/#shapevaluepath).

2. Bind the field name as `data.field` to the properties as [`shapeDataPath`](../api/maps/layerSettingsModel/#shapedatapath), [`colorValuePath`](../api/maps/markerSettingsModel/#colorvaluepath),
[`valuePath`](../api/maps/tooltipSettingsModel/#valuepath) and [`shapeValuePath`](../api/maps/markerSettingsModel/#shapevaluepath).

Refer complex support for data source as illustrated in the following example.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { Maps , Marker, Bubble, MapsTooltip } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(Marker, Bubble, MapsTooltip);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' >
    <e-layers>
    <e-layer  [shapeData]= 'shapeData'  [shapePropertyPath]= 'shapePropertyPath' [shapeDataPath]= 'shapeDataPath'
	[shapeSettings]='shapeSettings' [dataSource] = 'dataSource' [tooltipSettings]='tooltipSettings'
	[bubbleSettings]='bubbleSettings' [markerSettings]='markerSettings'></e-layer>
    </e-layers>
    </ejs-maps>`
})
export class AppComponent implements OnInit {
    public dataSource: object[];
    public shapeData: object;
    public shapePropertyPath: string;
    public shapeDataPath: string;
    public shapeSettings: object;
    public tooltipSettings: object;
    public bubbleSettings: object[];
    public markerSettings: object[];
    ngOnInit(): void {
        this.dataSource = [
			{ "Continent": "North America", 'color': '#71B081',
            data: { "continent": "North America", 'color': '#71B081' }
            },
            { "Continent": "South America", 'color': '#5A9A77',
            data: { "continent": "South America", 'color': '#5A9A77' }
            },
            { "Continent": "Africa", 'color': '#498770',
            data: { "continent": "Africa", 'color': '#498770' }
            },
            { "Continent": "Europe", 'color': '#39776C',
            data: { "continent": "Europe", 'color': '#39776C' }
            },
            { "Continent": "Asia", 'color': '#266665',
            data: { "continent": "Asia", 'color': '#266665' }
            },
            { "Continent": "Australia", 'color': '#124F5E',
            data: { "continent": "Australia", 'color': '#124F5E' }
            }
		]
        this.shapeData = world_map;
        this.shapePropertyPath = 'continent';
        this.shapeDataPath= 'data.continent';
	    this.shapeSettings = {
	       colorValuePath : 'data.color'
	    };
	    this.tooltipSettings = {
	        visible: true,
            valuePath: 'data.continent'
	    };
	    this.bubbleSettings =  [
            {
                visible: true,
                valuePath: 'data.value',
                colorValuePath: 'data.color',
                animationDuration: 0,
                minRadius: 20,
                maxRadius: 90,
                opacity: 0.8,
                dataSource: [
                    { 'name': 'India', 'value': 18.89685398845257, 'population': 391292635,
                    data: { 'color': 'red', 'population': 391292635, 'value': 189685398845257 }
                    }
                ],
                tooltipSettings: {
                    visible: true,
                    valuePath: 'data.population',
                    template:"<div>${data.population}</div>"
                }
            }
        ];
	    this.markerSettings = [
            {
                visible: true,
                dataSource: [
                    { latitude: 37.6276571, longitude: -122.4276688, name: 'San Bruno',
                    data: { x: 37.6276571, y: -122.4276688, name: 'San Bruno', shape: 'Pentagon',
                    color: 'red', imageUrl: 'images/ballon.png' }
                    },
                    { latitude: 33.5302186, longitude: -117.7418381, name: 'Laguna Niguel',
                    data: { x: 33.5302186, y: -117.7418381, name: 'Laguna Niguel', color: 'blue',
                    shape: 'Pentagon', imageUrl: 'images/ballon.png' }
                    }
                ],
                shapeValuePath: "data.shape",
                colorValuePath: "data.color",
                height: 20,
                width: 20,
                offset: {
                    y: -10,
                    x: 0
                },
                longitudeValuePath: "data.y",
                latitudeValuePath: "data.x",
                tooltipSettings: {
                    visible: true,
                    valuePath: 'data.name',
                    format: "${data.name}: ${data.x} : ${data.y}"
                },
                animationDuration: 0
            }
        ]
    };
}

```

{% endtab %}