# Populate Data

In this section you can learn how to populate shape data for providing Data input to Map control and usage of DataSource property.

## Shape Data

The Shape Data collection describing geographical shape information can be obtained from
[GEOJSON format shapes](http://files2.syncfusion.com/dtsupport/uploads/user/uploads/Maps_GeoJSON.zip).

.\ Maps_GeoJSON\All Countries with States

You can assign the complete contents in `“United States of America.json”` file to new JSON object. For better
understanding, a TS file `WorldMap.ts”` is already created to store JSON data in JSON object “usMap”.

`[WorldMap.ts]`

```typescript
export let usMap = //Paste all the content copied from the JSON file//
```

## Data Binding

The Maps control supports data binding with the `dataSource` property in the shape layers.

### Properties

The following properties in shape layers is be used for binding data in Maps control,

    * dataSource
    * shapeDataPath
    * shapePropertyPath

## Data Source

The dataSource property accepts the collection values as input. For example, you can provide the list of objects as input.

## Shape Data Path

The `shapeDataPath` property is used to refer the data ID in DataSource. For example, population MapData
contains data ids ‘Name’ and ‘Population’. The `shapeDataPath` and the `shapePropertyPath` properties are
related to each other (refer to `shapePropertyPath` for more details).

## Shape Property Path

The `shapePropertyPath` property is similar to the `shapeDataPath` that refers to the column name in the
`data` property of shape layers to identify the shape. When the values of the `shapeDataPath` property in the
`dataSource` property and the value of `shapePropertyPath` in the data property match, then the associated
object from the `dataSource` is bound to the corresponding shape.

The datasource is populated with JSON data relative to shape data and stored in JSON object. The WorldMap
population as datasource is used for better understanding.

The “populationData.ts” file is used to store JSON data in JSON object “populationData”.

Refer both shape data and datasource as illustrated in the following code example.

`[populationData.ts]`

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

[`app.component.ts`]

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
        public dataSource: Object[] = [ {
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
            },]
            public shapeData: Object = world_map;
    public shapePropertyPath: String = 'name';
    public shapeDataPath: String= 'name';
    };
}

```

{% endtab %}

<!-- markdownlint-disable MD010 -->

## Binding complex data source

You can bind the data field from data source to the maps in two different ways.

1. Bind the field name directly to the properties as [`shapeDataPath`](../api/maps/layerSettings/#shapedatapath), [`colorValuePath`](../api/maps/markerSettings/#colorvaluepath),
[`valuePath`](../api/maps/tooltipSettings/#valuepath) and [`shapeValuePath`](../api/maps/markerSettings/#shapevaluepath).

2. Bind the field name as `data.field` to the properties as [`shapeDataPath`](../api/maps/layerSettings/#shapedatapath), [`colorValuePath`](../api/maps/markerSettings/#colorvaluepath),
[`valuePath`](../api/maps/tooltipSettings/#valuepath) and [`shapeValuePath`](../api/maps/markerSettings/#shapevaluepath).

The complex data source binding can be done as illustrated in the following code example.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
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
    ngOnInit(): void {
        public dataSource: Object[] = [
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
            public shapeData: Object = world_map;
    public shapePropertyPath: String = 'continent';
    public shapeDataPath: String= 'data.continent';
	public shapeSettings: Object = {
	   colorValuePath : 'data.color'
	};
	public tooltipSettings: Object = {
	    visible: true,
            valuePath: 'data.continent'
	};
	public bubbleSettings: Object[] =  [
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
                },
            },
        ];
	public markerSettings: Object[] = [
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
            },
        ]
    };
}

```

{% endtab %}