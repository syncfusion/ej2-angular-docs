# Marker Type

## Add different types of markers

You can use different marker objects in maps control by using the marker settings.

To update different marker settings in maps, please follow the given steps:

**Step 1**:

Initialize the maps control with marker settings. Here, a marker has been added with specified latitude and
longitude of California by using the `dataSource` property. You can customize the shape of the marker using
the `Shape` property and change the border color and width of the marker using the `border` property as
mentioned in the following code example. To know more about the marker settings, please refer to the
[`API`](../../api/maps/markerSettings) documentation.

[`app.component.ts`]

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';
import { usa_map } from 'usa.ts';

@Component({
    selector: 'app-container',
    // specifies the template string for the maps component
    template:`<ejs-maps id='container'>
    <e-layers>
    <e-layer [shapeData]='usmap' [markerSettings]='markerSettings'></e-layer>
    </e-layers>
    </ejs-maps>`,
    encapsulation: ViewEncapsulation.None
  })
  export class AppComponent {
       public usmap=usa_map;
       public markerSettings = [
        {
            dataSource: [
                { latitude: 37.0000, longitude: -120.0000, city: 'California' }
            ],
            visible:true,
            shape:'Circle',
            fill:'white',
            width:3,
            animationDuration:0,
            border:{width:2,color:'#333'}
       }
    ]
}
```

{% endtab %}

**Step 2**:

Injecting MarkerService into NgModule

[`app.module.ts`]

```typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent }  from './app.component';
import { MapsModule, MarkerService } from '@syncfusion/ej2-angular-maps';

@NgModule({
  imports:      [ BrowserModule,MapsModule ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ],
  providers: [MarkerService]
})
export class AppModule { }
```

**Step 3**:

Customize the above option for n number of markers as mentioned in the following code example.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';
import { usa_map } from 'usa.ts';

@Component({
    selector: 'app-container',
    // specifies the template string for the maps component
    template:`<ejs-maps id='container'>
    <e-layers>
    <e-layer [shapeData]='usmap' [markerSettings]='markerSettings'></e-layer>
    </e-layers>
    </ejs-maps>`,
    encapsulation: ViewEncapsulation.None
  })
  export class AppComponent {
       public usmap=usa_map;
    //Initializing Map with Marker sttings
       public markerSettings = [
        {
            dataSource: [
                { latitude: 37.0000, longitude: -120.0000, city: 'California' }
            ],
            visible:true,
            shape:'Circle',
            fill:'white',
            width:3,
            animationDuration:0,
            border:{width:2,color:'#333'}
        },
        {
            dataSource: [
                { latitude: 40.7127, longitude: -74.0059, city: 'New York' }
            ],
            visible:true,
            shape:'Rectangle',
            fill:'yellow',
            width:15,
            height:4,
            animationDuration:0,
            border:{width:2,color:'#333'}
        },
        {
            dataSource: [
                { latitude: 42, longitude: -93, city: 'Iowa' }
            ],
            visible:true,
            shape:'Diamond',
            fill:'white',
            width:10,
            height:10,
            animationDuration:0,
            border:{width:2,color:'blue'}
        },
        {
            dataSource: [
                { latitude:36.499589049395055, longitude:-103.042108197135548, city:'New Mexico'}
            ],
            visible:true,
            shape:'Balloon',
            fill:'red',
            width:10,
            height:15,
            animationDuration:0,
            border:{width:2,color:'#333'}
        },
        {
            dataSource: [
                { latitude:36.360624205142919, longitude:-94.595916790727287, city:'Oklahoma'}
            ],
            visible:true,
            shape:'Triangle',
            fill:'blue',
            width:10,
            animationDuration:0,
            border:{width:2,color:'#333'}
        }
    ]
}
```

{% endtab %}

## Tooltip for Marker

Tooltip is used to display more information about marker on mouse over or touch end event. This can be
enabled separately for layer or marker by setting the `tooltipSettings.visible` property to **true**. The
`valuePath` property in tooltip takes the field name that presents in dataSource and displays that value as
tooltip text. The following code example illustrates enabling the tooltip for marker to show city name
field. To know more about tooltip, please refer to the [`API`](../../api/maps/tooltipSettings) documentation.

[`app.module.ts`]

```typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent }  from './app.component';
import { MapsModule } from '@syncfusion/ej2-angular-maps';
import { MapsTooltipService,MarkerService } from '@syncfusion/ej2-angular-maps';


@NgModule({
  imports:      [ BrowserModule,MapsModule ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ],
  providers:    [ MapsTooltipService,MarkerService ]
})
export class AppModule { }
```

[`app.component.ts`]

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';
import { usa_map } from 'usa.ts';

@Component({
    selector: 'app-container',
    // specifies the template string for the maps component
    template:`<div class="control-section">
    <div align='center'>
    <ejs-maps id='container' [height]='height' [width]='width' style="display:block;">
    <e-layers>
    <e-layer [shapeData]='usmap' [markerSettings]='markerSettings'></e-layer>
    </e-layers>
    </ejs-maps>
    </div>
    </div>`,
    encapsulation: ViewEncapsulation.None
  })
  export class AppComponent {
       public usmap = usa_map;
       public height='450px';
       public width='700px';
       public markerSettings = [{
        dataSource: [
            { latitude: 37.0000, longitude: -120.0000, city: 'California' }
        ],
        visible:true,
        shape:'Circle',
        fill:'white',
        width:3,
        animationDuration:0,
        border:{width:2,color:'#333'},
        tooltipSettings: {
            visible: true,
            valuePath:'city'
    }
       }]
}
```

{% endtab %}

```html
  <style>
          .markerTemplate {
            font-size: 12px;
            color: white;
            text-shadow: 0px 1px 1px black;
            font-weight: 500
          }
          .markerTemplate {
            height: 30px;
            width: 30px;
            display: block;
            margin: auto;
          }
  </style>
```