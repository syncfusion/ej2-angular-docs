# Navigation Lines

Navigation lines are used to denote the path between the two locations. We can use this feature as flight or train or sea routes.

## Customization

You can customize the following properties in the navigation lines by modifying their default values in `navigationlineSettings`

* Color - Specifies the color of navigation line.
* Dash array - Specifies the type of dash array line.
* Width - Specifies the line width.
* Angle - Specifies the navigation line angle.
* Highlight settings - Customizes the opacity, border, and fill color when the cursor hovers over it.
* Selection settings - Customizes the opacity, border, and fill color when the line is selected.

Following example shows rendering the path between two locations using latitudes and longitudes.

Yon can customize the navigation line color, dashArray, width and angle by modifying their default values in
`navigationLineSettings`.

Refer the below code snippet to navigate line between two cities in World map.
Import usmap geo json data from World.ts file.
Import the `NavigationLineService` and Inject into the Maps using `NgModule providers`.
Provide two locations latitude and longitude values to `navigationLineSettings`.

[`app.component.ts`]

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, ViewChild, OnInit } from '@angular/core';
import { Maps, NavigationLine } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(NavigationLine);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' >
    <e-layers>
    <e-layer  [shapeData]= 'shapeData' [navigationLineSettings] = 'navigationLineSettings' ></e-layer>
    </e-layers>
    </ejs-maps>`
})
export class AppComponent implements OnInit {
    ngOnInit(): void {
            public shapeData: Object = world_map;
            public navigationLineSettings: object[] = [{
            visible: true,
            latitude: [37.6276571, -122.4276688],
            longitude: [-74.0060, -117.7418381],
            color: 'black',
            angle: 90,
            width: 2,
            dashArray: '4'
        }],
    };
}

```

{% endtab %}

[`app.module.ts`]

Injecting NavigationLineService into NgModule.

```typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the MapsModule for the Maps component
import { MapsModule, NavigationLineService} from '@syncfusion/ej2-angular-maps';
import { AppComponent }  from './app.component';

@NgModule({
  // declaration of ej2-angular-maps module into NgModule
  imports:      [ BrowserModule, MapsModule ],
  declarations: [ AppComponent ],
  providers: [NavigationLineService],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## Enabling the arrows

You can enable the arrows in the navigation line using [`arrowSettings.showArrow`](../api/maps/arrow) API, also you can customize following properties in arrow

* color - Specifies the color of the arrow
* offset - Specifies the arrow's offset position
* position - Specifies the arrow position to `start` or `end` line
* size - Specifies the arrow size in pixel

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, ViewChild, OnInit } from '@angular/core';
import { Maps, NavigationLine } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(NavigationLine);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' >
    <e-layers>
    <e-layer  [shapeData]= 'shapeData' [navigationLineSettings] = 'navigationLineSettings' ></e-layer>
    </e-layers>
    </ejs-maps>`
})
export class AppComponent implements OnInit {
    ngOnInit(): void {
            public shapeData: Object = world_map;
            public navigationLineSettings: object[] = [{
            visible: true,
            latitude: [37.6276571, -122.4276688],
            longitude: [-74.0060, -117.7418381],
            color: 'black',
            angle: 90,
            width: 2,
            dashArray: '4',
            arrowSettings: {
              showArrow: true,
              size: 15,
              position: 'Start'
            }
        }],
    };
}

```

{% endtab %}

Refer the [`API`](../api/maps/navigationLineSettingsModel) for Navigation Lines feature.