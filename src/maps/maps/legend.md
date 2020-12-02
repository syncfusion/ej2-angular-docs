# Legend

A legend is a key used on a map that contains swatches of symbols with descriptions. It provides valuable
information for interpreting what the map is displaying and can be represented in various colors, shapes or
other identifiers based on the data. It gives a breakdown of what each symbol represents throughout the map.

## Visibility

The Legends can be made visible by setting the visible property of legendSettings to true.

## Positioning of the Legend

The legend can be positioned in two ways.

* Absolute Position.

* Dock Position.

### Absolute Position

Based on the margin values of X and Y-axes, the Map legends can be positioned with the support of `location.x`
and `location.y` properties available in legendSettings. For positioning the legend based on margins
corresponding to a map, position value is set as ‘Float’.

### Dock Position

The map legends can be positioned in following locations within the container.
You can set this option by using `position` property in legendSettings.

    1 Top

    2 Left

    3 Bottom

    4 Right

above four positions can be aligned combination of 'Near', 'Center' and 'Far' using `alignment` in
`legendSettings`. So legend can be aligned 12 positions.

## Legend Mode

Legend had two type of mode. `Default` mode and `Interactive` mode.

### Default Mode

Default mode legends having symbols with legend labels, used to identify the shape or bubble or marker color.

### Interactive Mode

The legends can be made interactive with an arrow mark indicating the exact range color in the legend when the
mouse hovers over the corresponding shapes. You can enable this option by setting `mode` property in
legendSettings value as “Interactive” and default value of `mode` property is “Default” to enable the normal legend.

## Legend Size

The map legend size can be modified by using the `height` and `width` properties in `legendSettings`.

## Legend for Shapes

The Layer shape type legends can be generated for each color mappings in shape settings.
**Note:** Below code snippet demonstrate the equal colormapping legends for the shapes.

Create the electiondata.ts file with following data for layer `dataSource`.

```typescript
export var electionData: Object[] =
[
    { value: 5, State: "Alabama", Candidate: "Trump", Trump:62.9,Clinton:34.6 },
    { value: 5, State: "Alaska", Candidate: "Trump", Trump:52.9,Clinton:37.7},
    { value: 5, State: "Arkansas", Candidate: "Trump", Trump:60.6,Clinton:33.7 },
    { value: 5, State: "Arizona", Candidate: "Trump", Trump:49.5,Clinton:45.4 },
    { value: 1, State: "California", Candidate: "Clinton", Trump:32.8,Clinton:61.6},
    { value: 1, State: "Colorado", Candidate: "Clinton", Trump:47.3,Clinton:44.4 },
    { value: 1, State: "Connecticut", Candidate: "Clinton", Trump:41.2,Clinton:54.5},
    { value: 1, State: "Delaware", Candidate: "Clinton", Trump:53.4,Clinton:41.9 },
    { value: 1, State: "District of Columbia",  Candidate: "Clinton", Trump:4.1,Clinton:92.8},
    { value: 5, State: "Florida", Candidate: "Trump", Trump:49.1,Clinton:47.8 },
    { value: 5, State: "Georgia", Candidate: "Trump", Trump:51.3,Clinton:45.6 },
    { value: 1, State: "Hawaii", Candidate: "Clinton", Trump:62.2,Clinton:30 },
    { value: 5, State: "Idaho", Candidate: "Trump", Trump:59.2,Clinton:27.6  },
    { value: 1, State: "Illinois", Candidate: "Clinton", Trump:55.4,Clinton:39.4  },
    { value: 5, State: "Indiana", Candidate: "Trump", Trump:57.2,Clinton:37.9  },
    { value: 5, State: "Iowa", Candidate: "Trump", Trump:51.8,Clinton:42.2  },
    { value: 5, State: "Kansas", Candidate: "Trump", Trump:57.2,Clinton:36.2 },
    { value: 5, State: "Kentucky", Candidate: "Trump", Trump:62.5,Clinton:32.7  },
    { value: 5, State: "Louisiana", Candidate: "Trump", Trump:58.1,Clinton:38.4  },
    { value: 1, State: "Maine", Candidate: "Clinton", Trump:45.2,Clinton:47.9 },
    { value: 1, State: "Maryland", Candidate: "Clinton", Trump:35.3,Clinton:60.5  },
    { value: 1, State: "Massachusetts", Candidate: "Clinton", Trump:33.5,Clinton:60.8 },
    { value: 5, State: "Michigan", Candidate: "Trump", Trump:47.6,Clinton:47.3  },
    { value: 1, State: "Minnesota", Candidate: "Clinton", Trump:45.4,Clinton:46.9 },
    { value: 5, State: "Mississippi", Candidate: "Trump", Trump:58.3,Clinton:39.7  },
    { value: 5, State: "Missouri", Candidate: "Trump", Trump:57.1,Clinton:38.0  },
    { value: 5, State: "Montana", Candidate: "Trump", Trump:56.5,Clinton:36.0 },
    { value: 5, State: "Nebraska", Candidate: "Trump", Trump:60.3,Clinton:34.0  },
    { value: 1, State: "Nevada", Candidate: "Clinton", Trump:45.5,Clinton:47.9  },
    { value: 1, State: "New Hampshire", Candidate: "Clinton", Trump:47.2,Clinton:47.6  },
    { value: 1, State: "New Jersey", Candidate: "Clinton", Trump:41.8,Clinton:55.0},
    { value: 1, State: "New Mexico", Candidate: "Clinton", Trump:40.0,Clinton:48.3  },
    { value: 1, State: "New York", Candidate: "Clinton", Trump:37.5,Clinton:58.8 },
    { value: 5, State: "North Carolina", Candidate: "Trump", Trump:50.5,Clinton:46.7 },
    { value: 5, State: "North Dakota", Candidate: "Trump", Trump:64.1,Clinton:27.8 },
    { value: 5, State: "Ohio", Candidate: "Trump", Trump:52.1,Clinton:43.5 },
    { value: 5, State: "Oklahoma", Candidate: "Trump", Trump:65.3,Clinton:28.9 },
    { value: 1, State: "Oregon", Candidate: "Clinton", Trump:41.1,Clinton:51.7  },
    { value: 5, State: "Pennsylvania", Candidate: "Trump", Trump:48.8,Clinton:47.6 },
    { value: 1, State: "Rhode Island", Candidate: "Clinton", Trump:39.8,Clinton:55.4 },
    { value: 5, State: "South Carolina", Candidate: "Trump", Trump:54.9,Clinton:40.8 },
    { value: 5, State: "South Dakota", Candidate: "Trump", Trump:61.5,Clinton:31.7 },
    { value: 5, State: "Tennessee", Candidate: "Trump", Trump:61.1,Clinton:34.9 },
    { value: 5, State: "Texas", Candidate: "Trump", Trump:52.6,Clinton:43.4  },
    { value: 5, State: "Utah", Candidate: "Trump", Trump:45.9,Clinton:27.8  },
    { value: 1, State: "Vermont", Candidate: "Clinton", Trump:39.7,Clinton:61.1  },
    { value: 1, State: "Virginia", Candidate: "Clinton", Trump:45.0,Clinton:49.9 },
    { value: 1, State: "Washington", Candidate: "Clinton", Trump:4.1,Clinton:92.8  },
    { value: 5, State: "Wisconsin", Candidate: "Trump", Trump:68.7,Clinton:26.5 },
    { value: 5, State: "West Virginia", Candidate: "Trump", Trump:47.9,Clinton:46.9  },
    { value: 5, State: "Wyoming", Candidate: "Trump", Trump:70.1,Clinton:22.5  }
    ];
```

Import the 'electionData' and assign for the layer `dataSource`. Provide the `shapePropertyPath` value as 'name
and `shapeDataPath` value as 'State'.

To enable the equal colormapping refer the `shapeSettings.colorMapping` code snippet.

Finally set `legendSettings.visible` as true and Inject the LegendService into NgModule using
`NgModule providers`.

[`app.component.ts`]

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

[`app.module.ts`]

Injecting `LegendService` to **NgModule**.

```typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the MapsModule for the Maps component
import { MapsModule, LegendService } from '@syncfusion/ej2-angular-maps';
import { AppComponent }  from './app.component';

@NgModule({
  // declaration of ej2-angular-maps module into NgModule
  imports:      [ BrowserModule, MapsModule ],
  declarations: [ AppComponent ],
  providers: [LegendService],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## Legend Shape

To get the legend shape value for `legendSettings` by using `shape` property. You can customize the shape
by using the `shapeWidth` and `shapeHeight` property.

## Legend for items excluded from color mapping

Based on the ranges in data source, get the excluded ranges from color mapping, and then show the legend with excluded range values are bound to the specific legend.

The following code example shows legends for the items excluded from color mapping.

[`app.component.ts`]

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
            {"Country": "Kazakhstan","Membership": "Both"},
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
                },
                {
                    color: 'violet'
                }
                ]
            };
            public legendSettings: Object = {
                visible: true
                }
   }
}

```

{% endtab %}

[`app.module.ts`]

Injecting `LegendService` to **NgModule**.

```typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the MapsModule for the Maps component
import { MapsModule, LegendService } from '@syncfusion/ej2-angular-maps';
import { AppComponent }  from './app.component';

@NgModule({
  // declaration of ej2-angular-maps module into NgModule
  imports:      [ BrowserModule, MapsModule ],
  declarations: [ AppComponent ],
  providers: [LegendService],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## Hide desired legend items

To enable or disable the desired legend for each colormapping, set the `showLegend` property to `true` in `colorMapping`.

The following code example shows legends for the items excluded from color mapping.

[`app.component.ts`]

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
            {"Country": "Kazakhstan","Membership": "Both"},
            { "Country": "Poland","Membership": "Non-Permanent"},
            {"Country": "Sweden","Membership": "Non-Permanent"}];
            public shapeData: Object = world_map;
            public shapePropertyPath: String = 'name';
            public shapeDataPath: String= 'Country';
            public shapeSettings: Object = {
                colorValuePath: 'Membership',
                colorMapping: [
                {
                    value: 'Permanent', color: '#D84444', showLegend : true
                },
                {
                    value: 'Non-Permanent', color: '#316DB5', showLegend : false
                },
                {
                    color: 'violet', showLegend : false
                }
                ]
            };
            public legendSettings: Object = {
                visible: true
                }
   }
}

```

{% endtab %}

[`app.module.ts`]

Injecting `LegendService` to **NgModule**.

```typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the MapsModule for the Maps component
import { MapsModule, LegendService } from '@syncfusion/ej2-angular-maps';
import { AppComponent }  from './app.component';

@NgModule({
  // declaration of ej2-angular-maps module into NgModule
  imports:      [ BrowserModule, MapsModule ],
  declarations: [ AppComponent ],
  providers: [LegendService],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## Hide legend items based data source value

To enable or disable the legend visibility for each item, bind the field name in the data source to the `showLegendPath` property in `legendSettings`.

The following code example shows how to hide the legend items based data source value.

[`app.component.ts`]

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
            public dataSource: Object[] = [{  "Country": "China", "Membership": "Permanent","visibility" : "true", "color" : "red"},
            {"Country": "France","Membership": "Permanent", "visibility" : "true", "color" : "blue" },
            { "Country": "Russia","Membership": "Permanent", "visibility" : "true", "color" : "green"},
            {"Country": "Kazakhstan","Membership": "Both", "visibility" : "true", "color" : "orange"},
            { "Country": "Poland","Membership": "Non-Permanent",
            "visibility" : "true", "color" : "yellow"},
            {"Country": "Sweden","Membership": "Non-Permanent",
            "visibility" : "true", "color" : "pink"}];
            public shapeData: Object = world_map;
            public shapePropertyPath: String = 'name';
            public shapeDataPath: String= 'Country';
            public shapeSettings: Object = {
                colorValuePath: 'color',
            };
            public legendSettings: Object = {
                visible: true,
                showLegendPath: 'visibility'
            }
   }
}

```

{% endtab %}

[`app.module.ts`]

Injecting `LegendService` to **NgModule**.

```typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the MapsModule for the Maps component
import { MapsModule, LegendService } from '@syncfusion/ej2-angular-maps';
import { AppComponent }  from './app.component';

@NgModule({
  // declaration of ej2-angular-maps module into NgModule
  imports:      [ BrowserModule, MapsModule ],
  declarations: [ AppComponent ],
  providers: [LegendService],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## Bind legend item text from data source

To show the legend text based on binding, the field name in the datasource should be set to the `valuePath` property in `legendSettings`.

The following code example shows how to hide the legend items based data source value.

[`app.component.ts`]

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
            public dataSource: Object[] = [{  "Country": "China", "Membership": "Permanent","visibility" : "true", "color" : "red"},
            {"Country": "France","Membership": "Permanent", "visibility" : "true", "color" : "blue" },
            { "Country": "Russia","Membership": "Permanent", "visibility" : "true", "color" : "green"},
            {"Country": "Kazakhstan","Membership": "Both", "visibility" : "true", "color" : "orange"},
            { "Country": "Poland","Membership": "Non-Permanent",
            "visibility" : "true", "color" : "yellow"},
            {"Country": "Sweden","Membership": "Non-Permanent",
            "visibility" : "true", "color" : "pink"}];
            public shapeData: Object = world_map;
            public shapePropertyPath: String = 'name';
            public shapeDataPath: String= 'Country';
            public shapeSettings: Object = {
                colorValuePath: 'color',
            };
            public legendSettings: Object = {
                visible: true,
                valuePath: 'Country'
            }
   }
}

```

{% endtab %}

[`app.module.ts`]

Injecting `LegendService` to **NgModule**.

```typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the MapsModule for the Maps component
import { MapsModule, LegendService } from '@syncfusion/ej2-angular-maps';
import { AppComponent }  from './app.component';

@NgModule({
  // declaration of ej2-angular-maps module into NgModule
  imports:      [ BrowserModule, MapsModule ],
  declarations: [ AppComponent ],
  providers: [LegendService],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## Hide duplicate legend items

To show the legend text based on binding, the field name in the datasource should be set to the `valuePath` property in `legendSettings`.

The following code example shows how to hide the legend items based data source value.

[`app.component.ts`]

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
            public dataSource: Object[] = [{  "Country": "China", "Membership": "Permanent","visibility" : "true", "color" : "red"},
            {"Country": "France","Membership": "Permanent", "visibility" : "true", "color" : "blue" },
            { "Country": "Russia","Membership": "Permanent", "visibility" : "true", "color" : "green"},
            {"Country": "Kazakhstan","Membership": "Both", "visibility" : "true", "color" : "orange"},
            { "Country": "Poland","Membership": "Non-Permanent",
            "visibility" : "true", "color" : "yellow"},
            {"Country": "Sweden","Membership": "Non-Permanent",
            "visibility" : "true", "color" : "pink"}];
            public shapeData: Object = world_map;
            public shapePropertyPath: String = 'name';
            public shapeDataPath: String= 'Country';
            public shapeSettings: Object = {
                colorValuePath: 'color',
            };
            public legendSettings: Object = {
                visible: true,
                valuePath: 'Membership',
                removeDuplicateLegend: true
            }
   }
}

```

{% endtab %}

[`app.module.ts`]

Injecting `LegendService` to **NgModule**.

```typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the MapsModule for the Maps component
import { MapsModule, LegendService } from '@syncfusion/ej2-angular-maps';
import { AppComponent }  from './app.component';

@NgModule({
  // declaration of ej2-angular-maps module into NgModule
  imports:      [ BrowserModule, MapsModule ],
  declarations: [ AppComponent ],
  providers: [LegendService],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## Toggle option in legend

The toggle option has been provided for legend. So, if you toggle a legend, the given color will be changed to the corresponding maps shape item. You can enable the toggle options using the `toggleLegendSettings` property.

The following options are available to customize the shape of the map:

* `applyShapeSettings` – Applies the fill property value in shapeSettings to a shape of the maps if it is true and a legend item is clicked.
* `fill`- Specifies the color to the shape of the maps.
* `opacity` – Specifies the transparency of the legend.
* `border` – Specifies the border color and width.

The following code example demonstrates how to add the toggle option to legend.

[`app.component.ts`]

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps, Legend } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
import{ Population_Density } from 'data.ts'

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
            public dataSource: Object[] = Population_Density;
            public shapeData: Object = world_map;
            public shapePropertyPath: String = 'name';
            public shapeDataPath: String= 'name';
            public shapeSettings: Object = {
                colorValuePath: 'density',
                colorMapping: [
                {
                    from: 0, to: 100, color: 'rgb(153,174,214)',
                },
                {
                    from: 101, to: 200, color: 'rgb(115,143,199)',
                },
                {
                    color: 'rgb(77,112,184)'
                }]
            };
            public legendSettings: Object = {
                visible: true,
                toggleLegendSettings: {
                enable: true,
                applyShapeSettings: false,
                border: {
                    color: 'green',
                    width: 2
                    }
                }
            }
        }
    }

```

{% endtab %}

[`app.module.ts`]

Injecting `LegendService` to **NgModule**.

```typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the MapsModule for the Maps component
import { MapsModule, LegendService } from '@syncfusion/ej2-angular-maps';
import { AppComponent }  from './app.component';

@NgModule({
  // declaration of ej2-angular-maps module into NgModule
  imports:      [ BrowserModule, MapsModule ],
  declarations: [ AppComponent ],
  providers: [LegendService],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

Refer the [`API`](../api/maps/legendSettingsModel) for Legend feature.