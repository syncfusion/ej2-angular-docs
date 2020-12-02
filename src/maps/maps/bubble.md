# Bubble

Bubbles in the Maps control represent the underlying data values of the map. Bubbles are scattered throughout
the map shapes that contains bound values.

Bubbles are included when data binding and the `bubbleSettings` is set to the shape layers.

To add bubbles to the map, bind data source to the layer `bubbleSeetings` and set the `valuePath` as
population. Following example illustrates bubble enable for the World map with **datasource**.
To render bubble in maps need to inject `BubbleService` module using `@NgModule providers` in `app.module.ts` file.

```typescript
export let world_map = // paste the World map from WorldMap.json Geo json file.
```

[`app.component.ts`]

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps, Bubble } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(Bubble);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container'  >
    <e-layers>
    <e-layer  [shapeData]= 'shapeData' [bubbleSettings] = 'bubbleSettings'></e-layer>
    </e-layers>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    ngOnInit(): void {
         public shapeData: Object = world_map;
         public shapeDataPath: Object = 'name',
         public shapePropertyPath: Object = 'name',
         public bubbleSettings: Object = [{
            visible: true,
            minRadius: 20,
            dataSource: [
                { name: 'India', population: '38332521' },
                { name: 'New Zealand', population: '19651127' },
                { name: 'Pakistan', population: '3090416' }
            ],
            maxRadius: 40,
            valuePath: 'population'
        }]
        public legendSettings: Object = {
        visible: true,
        type: 'Bubbles'
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
import { MapsModule, BubbleService } from '@syncfusion/ej2-angular-maps';
import { AppComponent }  from './app.component';

@NgModule({
  // declaration of ej2-angular-maps module into NgModule
  imports:      [ BrowserModule, MapsModule ],
  declarations: [ AppComponent ],
  providers: [BubbleService],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## Bubble Sizing

Using the `minRadius` and `maxRadius` properties in `bubbleSettings`, you can render the bubbles in different sizes based on the `valuePath` and `dataSource` values

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps, Bubble } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(Bubble);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container'  >
    <e-layers>
    <e-layer  [shapeData]= 'shapeData' [bubbleSettings] = 'bubbleSettings'></e-layer>
    </e-layers>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    ngOnInit(): void {
         public shapeData: Object = world_map;
         public shapeDataPath: Object = 'name',
         public shapePropertyPath: Object = 'name',
         public bubbleSettings: Object = [{
            visible: true,
            minRadius: 5,
            dataSource: [
                { name: 'India', population: '38332521' },
                { name: 'New Zealand', population: '19651127' },
                { name: 'Pakistan', population: '3090416' }
            ],
            maxRadius: 80,
            valuePath: 'population'
        }]
        public legendSettings: Object = {
        visible: true,
        type: 'Bubbles'
    };
   }
}
```

 {% endtab %}

## Multiple bubble groups

You can specify multiple types of bubble groups using the `bubbleSettings` property and customize it according to your requirement.

In the following code example, the gender-wise population ratio is demonstrated with two different bubble groups.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps, Bubble } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(Bubble);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container'  >
    <e-layers>
    <e-layer  [shapeData]= 'shapeData' [bubbleSettings] = 'bubbleSettings'></e-layer>
    </e-layers>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    ngOnInit(): void {
         public shapeData: Object = world_map;
         public shapeDataPath: Object = 'name',
         public shapePropertyPath: Object = 'name',
         public bubbleSettings: Object = [{
            visible: true,
            minRadius: 5,
            valuePath: "femaleRatio",
            colorValuePath: "femaleRatioColor",
            dataSource: [
                {
                    country: "United States", femaleRatio: 50.50442726, maleRatio: 49.49557274, femaleRatioColor: "green", maleRatioColor: "blue"
                },
                {
                    country: "India", femaleRatio: 48.18032713, maleRatio: 51.81967287, femaleRatioColor: "blue", maleRatioColor: "#c2d2d6"
                },
                {
                    country: "Oman", femaleRatio: 34.15597234, maleRatio: 65.84402766, femaleRatioColor: "#09156d", maleRatioColor: "orange"
                },
                {
                    country: "United Arab Emirates", femaleRatio: 27.59638942, maleRatio: 72.40361058, femaleRatioColor: "#09156d", maleRatioColor: "orange"
                }
            ],
            maxRadius: 20,
        },
        {
            visible: true,
            bubbleType: 'Circle',
            opacity: 0.4,
            minRadius: 15,
            valuePath: "maleRatio",
            colorValuePath: "maleRatioColor",
            dataSource: [
                {
                    country: "United States", femaleRatio: 50.50442726, maleRatio: 49.49557274, femaleRatioColor: "green", maleRatioColor: "blue"
                },
                {
                    country: "India", femaleRatio: 48.18032713, maleRatio: 51.81967287, femaleRatioColor: "blue", maleRatioColor: "#c2d2d6"
                },
                {
                    country: "Oman", femaleRatio: 34.15597234, maleRatio: 65.84402766, femaleRatioColor: "#09156d", maleRatioColor: "orange"
                },
                {
                    country: "United Arab Emirates", femaleRatio: 27.59638942, maleRatio: 72.40361058, femaleRatioColor: "#09156d", maleRatioColor: "orange"
                }
            ],
            maxRadius: 25,
        }]
        public legendSettings: Object = {
            visible: true,
            type: 'Bubbles'
    };
   }
}
```

{% endtab %}

## Enable Legend for Bubble

To enable the legend for the bubble, need to set `legendSettings.visible` as true and `legendSettings.type` as
'Bubbles'. To render the legend in maps need to Inject `LegendService` using `@NgModule providers` in `app.module.ts` file.
Refer the below code snippet to enable the legend for bubbles with each bubble different colors rendering.

[`app.component.ts`]

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps, Bubble, Legend } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(Bubble, Legend);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container'  [legendSettings] ='legendSettings'  >
    <e-layers>
    <e-layer  [shapeData]= 'shapeData' [bubbleSettings] = 'bubbleSettings'></e-layer>
    </e-layers>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    ngOnInit(): void {
         public shapeData: Object = world_map;
         public shapeDataPath: Object = 'name',
         public shapePropertyPath: Object = 'name',
         public bubbleSettings: Object = [{
            visible: true,
            minRadius: 20,
            dataSource:  [
                {color: 'green', name: 'India', population: '38332521' },
                {color: 'purple', name: 'New Zealand', population: '19651127' },
                {color: 'blue', name: 'Pakistan', population: '3090416' }
            ],
            maxRadius: 40,
            valuePath: 'population'
        }];
        public legendSettings: Object = {
        visible: true,
        type: 'Bubbles'
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
import { MapsModule, BubbleService, LegendService } from '@syncfusion/ej2-angular-maps';
import { AppComponent }  from './app.component';

@NgModule({
  // declaration of ej2-angular-maps module into NgModule
  imports:      [ BrowserModule, MapsModule ],
  declarations: [ AppComponent ],
  providers: [BubbleService, LegendService],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

Refer the [`API`](../api/maps/bubbleSettingsModel) for Bubble feature.