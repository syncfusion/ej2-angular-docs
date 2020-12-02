# ColorMapping

ColorMapping used to customize the shape colors based given values. It has three types: range color mapping, equal color mapping and desaturation color mapping.

## Range color mapping

Range color mapping applied by the mapped value is numeric and with in the given color mapping ranges provided
in the `dataSource`. Refer the below dataSource for the population density of some countries.

[`PopulationDensity.ts`]

```typescript
export let population_density = [
    ...
    {
        'code': 'AE',
        'value': 90,
        'name': 'United Arab Emirates',
        'population': 8264070,
        'density': 99
    },
    {
        'code': 'GB',
        'value': 257,
        'name': 'United Kingdom',
        'population': 62041708,
        'density': 255
    },
    {
        'code': 'US',
        'value': 34,
        'name': 'United States',
        'population': 325020000,
        'density': 33
    }
    ...
    ];
```

Bind the `population_density` value to layer `dataSource` and specify the `colorValuePath` as 'density' to map the range value for shapes.
Create `worldmap` data from GeoJSON.
Refer the code snippet below.

[`app.component.ts`]

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
import { Population_Density } from 'data.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container'  >
    <e-layers>
    <e-layer  [shapeData]= 'shapeData' [shapeDataPath] = 'shapeDataPath' [shapePropertyPath] ='shapePropertyPath' [shapeSettings] = 'shapeSettings' [dataSource] ='dataSource'></e-layer>
    </e-layers>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    ngOnInit(): void {
         public shapeData: Object = world_map;
         public shapeDataPath: String = 'name';
         public shapePropertyPath : String= 'name';
        public dataSource : Object[]= Population_Density;
         public shapeSettings: Object = {
           colorValuePath: 'density',
            fill: '#E5E5E5',
            colorMapping: [
                {
                    from: 0.00001, to: 100, color: 'rgb(153,174,214)'
                },
                {
                    from: 100, to: 200, color: 'rgb(115,143,199)'
                },
                {
                    from: 200, to: 300, color: 'rgb(77,112,184)'
                },
                {
                    from: 300, to: 500, color: 'rgb(38,82,168)'
                },
                {
                    from: 500, to: 19000, color: 'rgb(0,51,153)'
                }
            ]
            };
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

## Equal color mapping

Equal color mapping used to apply color mapping if the mapped value is string.
Following example demonstrate the permanent and non-permanent countries in the UN security council, in 2017. Refer the below dataSource.

```typescript
export let unCountries: object[] = [
{ Country: 'China', Membership: 'Permanent' },
{ Country: 'France', Membership: 'Permanent' },
{ Country: 'Russia', Membership: 'Permanent' },
{ Country: 'United Kingdom', Membership: 'Permanent' },
{ Country: 'United States', Membership: 'Permanent' },
{ Country: 'Bolivia', Membership: 'Non-Permanent' },
{ Country: 'Eq. Guinea', Membership: 'Non-Permanent' },
{ Country: 'Ethiopia', Membership: 'Non-Permanent' },
{ Country: "Côte d'Ivoire", Membership: 'Permanent' },
{ Country: 'Kazakhstan', Membership: 'Non-Permanent' },
{ Country: 'Kuwait', Membership: 'Non-Permanent' },
{ Country: 'Netherlands', Membership: 'Non-Permanent' },
{ Country: 'Peru', Membership: 'Non-Permanent' },
{ Country: 'Poland', Membership: 'Non-Permanent' },
{ Country: 'Sweden', Membership: 'Non-Permanent' },
];
```

Bind the unCountries data to the layer dataSource property and set the shapeSettings `colorValuePath` as
'Membership' and set the colorMapping values to that. Refer the below code snippet.

[`app.component.ts`]

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
import { unCountries } from 'data.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container'  >
    <e-layers>
    <e-layer  [shapeData]= 'shapeData' [shapeDataPath] = 'shapeDataPath' [shapePropertyPath] ='shapePropertyPath' [shapeSettings] = 'shapeSettings' [dataSource] ='dataSource'></e-layer>
    </e-layers>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    ngOnInit(): void {
         public shapeData: Object = world_map;
         public shapeDataPath: String = 'Country';
         public shapePropertyPath : String= 'name';
        public dataSource : Object[]= unCountries;
         public shapeSettings: Object = {
            fill: '#E5E5E5',
            colorMapping: [
                {
                    value: 'Permanent',
                    color: '#C3E6ED'
                },
                {
                    color: '#F1931B',
                    value: 'Non-Permanent'
                }
            ],
            colorValuePath: 'Membership'
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

## Desaturation color mapping

Desaturation color mapping is used to apply colors with opacity to shapes based on the given values for the `minOpacity` and `maxOpacity` properties in the map control.

The following code example shows how to apply desaturation color mapping to shapes.

[`PopulationDensity.ts`]

```typescript
export let population_density = [
    ...
    {
        'code': 'AE',
        'value': 90,
        'name': 'United Arab Emirates',
        'population': 8264070,
        'density': 99
    },
    {
        'code': 'GB',
        'value': 257,
        'name': 'United Kingdom',
        'population': 62041708,
        'density': 255
    },
    {
        'code': 'US',
        'value': 34,
        'name': 'United States',
        'population': 325020000,
        'density': 33
    }
    ...
    ];
```

Bind the `population_density` value to layer `dataSource` and specify the `colorValuePath` as 'density' to map the range value for shapes.
Create `worldmap` data from GeoJSON.
Refer the code snippet below.

[`app.component.ts`]

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
import { Population_Density } from 'data.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container'  >
    <e-layers>
    <e-layer  [shapeData]= 'shapeData' [shapeDataPath] = 'shapeDataPath' [shapePropertyPath] ='shapePropertyPath' [shapeSettings] = 'shapeSettings' [dataSource] ='dataSource'></e-layer>
    </e-layers>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    ngOnInit(): void {
         public shapeData: Object = world_map;
         public shapeDataPath: String = 'name';
         public shapePropertyPath : String= 'name';
        public dataSource : Object[]= Population_Density;
         public shapeSettings: Object = {
           colorValuePath: 'density',
            fill: '#E5E5E5',
            colorMapping: [
                {
                    from: 0, to: 100, minOpacity: 0.4, maxOpacity: 1, color: 'rgb(153,174,214)'
                },
                {
                    from: 101, to: 200, minOpacity: 0.7, maxOpacity: 1, color: 'rgb(115,143,199)'
                },
            ]
            };
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

## Desaturation with multiple colors

Multiple colors are used as gradient effect to the specific shapes based on the ranges in the datasource.

By using color API, you can set n number of colors.

The following code example shows how to use multiple colors.

[`PopulationDensity.ts`]

```typescript
export let population_density = [
    ...
    {
        'code': 'AE',
        'value': 90,
        'name': 'United Arab Emirates',
        'population': 8264070,
        'density': 99
    },
    {
        'code': 'GB',
        'value': 257,
        'name': 'United Kingdom',
        'population': 62041708,
        'density': 255
    },
    {
        'code': 'US',
        'value': 34,
        'name': 'United States',
        'population': 325020000,
        'density': 33
    }
    ...
    ];
```

Bind the `population_density` value to layer `dataSource` and specify the `colorValuePath` as 'density' to map the range value for shapes.
Create `worldmap` data from GeoJSON.
Refer the code snippet below.

[`app.component.ts`]

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
import { Population_Density } from 'data.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container'  >
    <e-layers>
    <e-layer  [shapeData]= 'shapeData' [shapeDataPath] = 'shapeDataPath' [shapePropertyPath] ='shapePropertyPath' [shapeSettings] = 'shapeSettings' [dataSource] ='dataSource'></e-layer>
    </e-layers>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    ngOnInit(): void {
         public shapeData: Object = world_map;
         public shapeDataPath: String = 'name';
         public shapePropertyPath : String= 'name';
        public dataSource : Object[]= Population_Density;
         public shapeSettings: Object = {
           colorValuePath: 'density',
            fill: '#E5E5E5',
            colorMapping: [
                {
                    from: 0, to: 100, color: ['red', 'blue']
                },
                {
                    from: 101, to: 200, color: ['green','violet']
                },
            ]
            };
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

## Color for items excluded from color mapping

You will map the colors to the shapes based on the ranges or values in the data source records may have been excluded from the color mapping configuration, in which case you may also add the color for excluded items.

The following code example shows how to set the color for items excluded from color mapping.

[`PopulationDensity.ts`]

```typescript
export let population_density = [
    ...
    {
        'code': 'AE',
        'value': 90,
        'name': 'United Arab Emirates',
        'population': 8264070,
        'density': 99
    },
    {
        'code': 'GB',
        'value': 257,
        'name': 'United Kingdom',
        'population': 62041708,
        'density': 255
    },
    {
        'code': 'US',
        'value': 34,
        'name': 'United States',
        'population': 325020000,
        'density': 33
    }
    ...
    ];
```

In following code example, You have added color mapping for the ranges from 0 to 200. If we have any records in the data source beyond this range, color mapping will not be applied. To apply the color for these excluded items, set `color` value in the `colorMapping` with out range or value.

[`app.component.ts`]

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
import { Population_Density } from 'data.ts';

@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container'  >
    <e-layers>
    <e-layer  [shapeData]= 'shapeData' [shapeDataPath] = 'shapeDataPath' [shapePropertyPath] ='shapePropertyPath' [shapeSettings] = 'shapeSettings' [dataSource] ='dataSource'></e-layer>
    </e-layers>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    ngOnInit(): void {
         public shapeData: Object = world_map;
         public shapeDataPath: String = 'name';
         public shapePropertyPath : String= 'name';
        public dataSource : Object[]= Population_Density;
         public shapeSettings: Object = {
           colorValuePath: 'density',
            fill: '#E5E5E5',
            colorMapping: [
                {
                    from: 0, to: 100, color: 'red'
                },
                {
                    from: 101, to: 200, color: 'green'
                },
                {
                    color: 'violet'
                }
            ]
            };
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

Refer the [`API`](../api/maps/colorMappingSettingsModel) for Color Mapping feature.