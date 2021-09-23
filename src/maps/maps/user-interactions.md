---
title: "User interactions in Angular Maps control | Syncfusion"

component: "Maps"

description: "Learn here all about User interactions of Syncfusion Angular Maps control and more."
---

# User Interactions in Angular Maps control

## Zooming

The zooming feature is used to zoom in and out of Maps to show in-depth information. It is controlled by the [`zoomFactor`](../api/maps/zoomSettingsModel/#zoomfactor) property of the [`zoomSettings`](../api/maps/zoomSettingsModel). The [`zoomFactor`](../api/maps/zoomSettingsModel/#zoomfactor) is increased or decrease dynamically based on zoom in and out interaction.

<b>Enable zooming</b>

Zooming of Maps is enabled by setting the [`enable`](../api/maps/zoomSettingsModel/#enable) property of [`zoomSettings`](../api/maps/zoomSettingsModel/) to **true**.

<!-- markdownlint-disable MD010 -->

<b>Enable panning</b>

To enable the panning feature, set the [`enablePanning`](../api/maps/zoomSettingsModel/#enablepanning) property of [`zoomSettings`](../api/maps/zoomSettingsModel) to **true**.

<b>app.component.ts</b>

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { Maps, Zoom } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(Zoom);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' [zoomSettings] = 'zoomSettings'>
     <e-layers>
    <e-layer [shapeData] = 'shapeData'></e-layer>
    </e-layers>
    </ejs-maps>`
})
export class AppComponent implements OnInit {
    public zoomSettings: object;
    public shapeData: object;
    ngOnInit(): void {
        this.zoomSettings = {
            enable: true,
		    enablePanning: true
        };
        this.shapeData = world_map;
    }
}

```

{% endtab %}

**app.module.ts**
Injecting ZoomService into NgModule.

```typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the MapsModule for the Maps component
import { MapsModule, ZoomService} from '@syncfusion/ej2-angular-maps';
import { AppComponent }  from './app.component';

@NgModule({
  // declaration of ej2-angular-maps module into NgModule
  imports:      [ BrowserModule, MapsModule ],
  declarations: [ AppComponent ],
  providers: [ZoomService],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

### Various type of zooming

Zooming can be performed in following types:

#### Zooming toolbar

The following options are available in toolbar.

1. Zoom - Provides rectangular zoom support.
2. ZoomIn - Zooms in the Maps.
3. ZoomOut - Zooms out the Maps.
4. Pan - Switches to panning if rectangular zoom is activated.
5. Reset - Restores the Maps to the default view.

The following properties are available in toolbars to customize the zooming toolbars.

* [`color`](../api/maps/zoomSettingsModel/#color) - To apply the color for toolbars in Maps.
* [`highlightColor`](../api/maps/zoomSettingsModel/#highlightcolor) - To apply the color for the zooming toolbar when the mouse has hovered on the toolbar element in Maps.
* [`horizontalAlignment`](../api/maps/zoomSettingsModel/#horizontalalignment) - To customize the position type of toolbar when it is placed horizontally.
* [`selectionColor`](../api/maps/zoomSettingsModel/#selectioncolor) - To apply the color for the zooming toolbar when clicking the zooming toolbar in Maps.
* [`toolBarOrientation`](../api/maps/zoomSettingsModel/#toolbarorientation) - To customize the orientation of the zooming toolbar.
* [`toolbars`](../api/maps/zoomSettingsModel/#toolbars) - To customize the items that are to be shown in the zooming toolbar in Maps.
* [`verticalAlignment`](../api/maps/zoomSettingsModel/#verticalalignment) - To customize the position type of toolbar when it is placed vertically.

``` typescript
import { Component, OnInit } from '@angular/core';
import { Maps, Zoom } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(Zoom);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' [zoomSettings] = 'zoomSettings'>
     <e-layers>
    <e-layer [shapeData] = 'shapeData'></e-layer>
    </e-layers>
    </ejs-maps>`
})
export class AppComponent implements OnInit {
    public zoomSettings: object;
    public shapeData: object;
    ngOnInit(): void {
        this.zoomSettings = {
            enable: true,
            color: 'green',
            highlightColor: 'blue',
            selectionColor: 'orange',
            horizontalAlignment: 'Center',
            toolbars: ['ZoomIn', 'ZoomOut', 'Pan', 'Reset']
        };
        this.shapeData = world_map;
    }
}

```

#### Pinch zooming

To enable or disable the pinch zooming, use the [`pinchZooming`](../api/maps/zoomSettingsModel/#pinchzooming) property in [`zoomSettings`](../api/maps/zoomSettingsModel).

``` typescript
import { Component, OnInit } from '@angular/core';
import { Maps, Zoom } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(Zoom);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' [zoomSettings] = 'zoomSettings'>
     <e-layers>
    <e-layer [shapeData] = 'shapeData'></e-layer>
    </e-layers>
    </ejs-maps>`
})
export class AppComponent implements OnInit {
    public zoomSettings: object;
    public shapeData: object;
    ngOnInit(): void {
        this.zoomSettings = {
            enable: true,
            pinchZooming:true
        };
        this.shapeData = world_map;
    }
}

```

#### Single-click zooming

To enable or disable the single-click zooming, use the [`zoomOnClick`](../api/maps/zoomSettingsModel/#zoomonclick) property in [`zoomSettings`](../api/maps/zoomSettingsModel).

``` typescript
import { Component, OnInit } from '@angular/core';
import { Maps, Zoom } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(Zoom);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' [zoomSettings] = 'zoomSettings'>
     <e-layers>
    <e-layer [shapeData] = 'shapeData'></e-layer>
    </e-layers>
    </ejs-maps>`
})
export class AppComponent implements OnInit {
    public zoomSettings: object;
     public shapeData: object;
    ngOnInit(): void {
        this.zoomSettings = {
            enable: true,
            zoomOnClick:true
        };
        this.shapeData = world_map;
    }
}

```

#### Double-click zooming

To enable or disable the double-click zooming, use the [`doubleClickZoom`](../api/maps/zoomSettingsModel/#doubleclickzoom) property in [`zoomSettings`](../api/maps/zoomSettingsModel/).

``` typescript
import { Component, OnInit } from '@angular/core';
import { Maps, Zoom } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(Zoom);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' [zoomSettings] = 'zoomSettings'>
     <e-layers>
    <e-layer [shapeData] = 'shapeData'></e-layer>
    </e-layers>
    </ejs-maps>`
})
export class AppComponent implements OnInit {
    public zoomSettings: object;
    public shapeData: object;
    ngOnInit(): void {
        this.zoomSettings = {
            enable: true,
            doubleClickZoom:true
        };
        this.shapeData = world_map;
    }
}

```

#### Mouse wheel zooming

To enable or disable mouse wheel zooming, use the [`mouseWheelZoom`](../api/maps/zoomSettingsModel/#mousewheelzoom) property in [`zoomSettings`](../api/maps/zoomSettingsModel/).

``` typescript
import { Component, OnInit } from '@angular/core';
import { Maps, Zoom } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(Zoom);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' [zoomSettings] = 'zoomSettings'>
     <e-layers>
    <e-layer [shapeData] = 'shapeData'></e-layer>
    </e-layers>
    </ejs-maps>`
})
export class AppComponent implements OnInit {
    public zoomSettings: object;
    public shapeData: object;
    ngOnInit(): void {
        this.zoomSettings = {
            enable: true,
            mouseWheelZoom:true
        };
        this.shapeData = world_map;
    }
}

```

#### Selection zooming

To enable or disable selection zooming, use the [`enableSelectionZooming`](../api/maps/zoomSettingsModel/#enableselectionzooming) property in [`zoomSettings`](../api/maps/zoomSettingsModel/). The [`enablePanning`](../api/maps/zoomSettingsModel/#enablepanning) property must be set to **false** to enable the selection zooming in Maps.

``` typescript
import { Component, OnInit } from '@angular/core';
import { Maps, Zoom } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(Zoom);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' [zoomSettings] = 'zoomSettings'>
     <e-layers>
    <e-layer [shapeData] = 'shapeData'></e-layer>
    </e-layers>
    </ejs-maps>`
})
export class AppComponent implements OnInit {
    public zoomSettings: object;
    public shapeData: object;
    ngOnInit(): void {
        this.zoomSettings = {
            enable: true,
            enableSelectionZooming: true,
            enablePanning: false
        };
        this.shapeData = world_map;
    }
}

```

### Setting minimum and maximum values for zoom factor

The zooming range can be adjusted using the [`minZoom`](../api/maps/zoomSettingsModel/#minzoom) and [`maxZoom`](../api/maps/zoomSettingsModel/#maxzoom) properties in [`zoomSettings`](../api/maps/zoomSettingsModel/). The minZoom value is set to 1 by default, and the maxZoom value is set to 10.

``` typescript
import { Component, OnInit } from '@angular/core';
import { Maps, Zoom } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(Zoom);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' [zoomSettings] = 'zoomSettings'>
     <e-layers>
    <e-layer [shapeData] = 'shapeData'></e-layer>
    </e-layers>
    </ejs-maps>`
})
export class AppComponent implements OnInit {
    public zoomSettings: object;
    public shapeData: object;
    ngOnInit(): void {
        this.zoomSettings = {
            enable: true,
            minZoom: 2,
            maxZoom: 12
        };
        this.shapeData = world_map;
    }
}

```

### Zooming with animation

To zoom in or zoom out the Maps with animation, use the [`animationDuration`](../api/maps/layerSettingsModel/#animationduration) property in [`layers`](../api/maps/layerSettingsModel).

``` typescript
import { Component, OnInit } from '@angular/core';
import { Maps, Zoom } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(Zoom);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' [zoomSettings] = 'zoomSettings'>
     <e-layers>
    <e-layer [shapeData] = 'shapeData' [animationDuration] = 'animationDuration'></e-layer>
    </e-layers>
    </ejs-maps>`
})
export class AppComponent implements OnInit {
    public zoomSettings: object;
    public shapeData: object;
    public animationDuration: number;
    ngOnInit(): void {
        this.zoomSettings = {
            enable: true,
            mouseWheelZoom:true
        };
        this.animationDuration = 500;
        this.shapeData = world_map;
    }
}

```

<b>app.component.ts</b>

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { Maps, Zoom } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(Zoom);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' [zoomSettings] = 'zoomSettings'>
     <e-layers>
    <e-layer [shapeData] = 'shapeData'></e-layer>
    </e-layers>
    </ejs-maps>`
})
export class AppComponent implements OnInit {
    public zoomSettings: object;
    public shapeData: object;
    ngOnInit(): void {
        this.zoomSettings = {
        enable: true,
    };
        this.shapeData = world_map;
    }
}

```

{% endtab %}

## Selection

Each shape in the Maps can be selected and deselected during interaction with the shapes. Selection is enabled by setting the [`enable`](../api/maps/selectionSettingsModel/#enable) property of [`selectionSettings`](../api/maps/selectionSettingsModel) to **true**.

The following properties are available to customize the selection of Maps elements such as shapes, bubbles, markers and legends.

* [`border`](../api/maps/selectionSettingsModel/#border) - To customize the color, width and opacity of the border of which element is selected in Maps.
* [`fill`](../api/maps/selectionSettingsModel/#fill) - Applies the color for the element that is selected.
* [`opacity`](../api/maps/selectionSettingsModel/#opacity) - To customize the transparency for the element that is selected.
* [`enableMultiSelect`](../api/maps/selectionSettingsModel/#enablemultiselect) - To enable or disable the selection for multiple shapes or markers or bubbles in the Maps.

By tapping on the specific legend, the shapes which are bounded to the selected legend is also selected and vice versa.

<b>app.component.ts</b>

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { Maps, Selection, Legend } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(Selection, Legend);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' [legendSettings]='legendSettings'>
     <e-layers>
    <e-layer [shapeData] = 'shapeData' [shapePropertyPath]='shapePropertyPath' [shapeDataPath]='shapeDataPath' [dataSource]='dataSource' [shapeSettings]='shapeSettings' [selectionSettings] ='selectionSettings'></e-layer>
    </e-layers>
    </ejs-maps>`
})
export class AppComponent implements OnInit {
    public selectionSettings: object;
    public shapeData: object;
    public shapePropertyPath: string;
    public shapeDataPath: string;
    public dataSource: object;
    public shapeSettings: object;
    public legendSettings: object;
    ngOnInit(): void {
        this.selectionSettings = {
            enable: true,
            fill: 'blue',
            border: { color: 'white', width: 2}
        };
        this.shapeData = world_map;
        this.shapePropertyPath = "name";
        this.shapeDataPath = "Country";
        this.dataSource = [
            {  "Country": "China", "Membership": "Permanent"},
            { "Country": "France","Membership": "Permanent" },
            { "Country": "Russia","Membership": "Permanent"},
            { "Country": "Kazakhstan","Membership": "Non-Permanent"},
            { "Country": "Poland","Membership": "Non-Permanent"},
            { "Country": "Sweden","Membership": "Non-Permanent"}
        ];
        this.shapeSettings = {
            colorValuePath: 'Membership',
                colorMapping: [
                    {
                        value: 'Permanent', color: '#D84444'
                    },
                    {
                        value: 'Non-Permanent', color: '#316DB5'
                   }]
        };
        this.legendSettings = {
            visible: true
    }
}
}

```

{% endtab %}

### Enable selection for bubbles

To enable the selection for bubbles in Maps, set the [`selectionSettings`](../api/maps/selectionSettingsModel) in [`bubbleSettings`](../api/maps/bubbleSettingsModel/) and set the [`enable`](../api/maps/selectionSettingsModel/#enable) property of [`selectionSettings`](../api/maps/selectionSettingsModel) as **true**.

>To use the bubble feature, the Bubble module must be injected.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { Maps, Bubble, Selection } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(Bubble, Selection);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container'>
    <e-layers>
    <e-layer  [shapeData]= 'shapeData' [bubbleSettings] = 'bubbleSettings'></e-layer>
    </e-layers>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    public shapeData: object;
    public shapeDataPath: object;
    public shapePropertyPath: object;
    public bubbleSettings: object;
    ngOnInit(): void {
        this.shapeData = world_map;
        this.shapeDataPath = 'name',
        this.shapePropertyPath = 'name',
        this.bubbleSettings = [{
            visible: true,
            dataSource: [
                { name: 'India', population: '38332521' },
                { name: 'South Africa', population: '19651127' },
                { name: 'Pakistan', population: '3090416' }
            ],
            selectionSettings: {
                enable: true,
                fill: 'green',
                border: { color: 'white', width: 2}
            },
            valuePath: 'population'
        }]
    }
}
```

 {% endtab %}

### Enable selection for markers

To enable the selection for markers in Maps, set the [`selectionSettings`](../api/maps/selectionSettingsModel) in the [`markerSettings`](../api/maps/markerSettingsModel) and set the [`enable`](../api/maps/selectionSettingsModel/#enable) property of the [`selectionSettings`](../api/maps/selectionSettingsModel) as **true**.

>To use the marker feature, the Marker module must be injected.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { Maps, Marker, Selection } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(Marker, Selection);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container'>
    <e-layers>
    <e-layer  [shapeData]= 'shapeData' [markerSettings] = 'markerSettings'></e-layer>
    </e-layers>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    public shapeData: object;
    public markerSettings: object;
    ngOnInit(): void {
        this.shapeData = world_map;
        this.markerSettings = [{
           visible: true,
            height: 20,
            width: 20,
            fill: 'green',
            shape:'Balloon',
            selectionSettings: {
                enable: true,
                fill: 'blue',
                border: { color: 'white', width: 2}
            },
            dataSource: [
                { latitude: 49.95121990866204, longitude: 18.468749999999998, name:'Europe' },
                { latitude: 59.88893689676585, longitude: -109.3359375, name:'North America'},
                { latitude: -6.64607562172573, longitude: -55.54687499999999, name:'South America'}
            ]
        }];
    }
}
```

{% endtab %}

### Public method for the shape selection

The [`shapeSelection`](../api/maps/#shapeselection) method can be used to select each shape in the Maps.
LayerIndex, propertyName, country name, and selected value as a boolean state(true / false) are the input parameters for this method.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps, Selection, MapsComponent} from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(Selection);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' #maps>
    <e-layers>
    <e-layer  [shapeData]= 'shapeData' [selectionSettings] ='selectionSettings'></e-layer>
    </e-layers>
    </ejs-maps> <button  id='select' (click)='select()'>select</button> <button id='unselect' (click)='unselect()'>unselect</button>`
})

export class AppComponent {
    @ViewChild('maps')
    public mapObj: MapsComponent;
    public shapeData: object = world_map;
    public selectionSettings: object = {
        enable: true,
        fill: 'green',
        border: { color: 'white', width: 2 }
    };
    select(){
        this.mapObj.shapeSelection(0, "continent", "Asia", true);
    };
    unselect(){
        this.mapObj.shapeSelection(0, "continent", "Asia", false);
    }
}
```

 {% endtab %}

### Initial shape selection

The shape is initially selected using the [`initialShapeSelection`](../api/maps/initialShapeSelectionSettingsModel), and the values are mapped to the [`shapePath`](../api/maps/initialShapeSelectionSettingsModel/#shapepath) and [`shapeValue`](../api/maps/initialShapeSelectionSettingsModel/#shapevalue).

>initialShapeSelection is an Array property.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { Maps, Selection} from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(Selection);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' >
    <e-layers>
    <e-layer  [shapeData]= 'shapeData' [initialShapeSelection] = 'initialShapeSelection' [selectionSettings] ='selectionSettings'></e-layer>
    </e-layers>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    public shapeData: object;
    public initialShapeSelection: object;
    public selectionSettings: object;
    ngOnInit(): void {
        this.shapeData = world_map;
        this.initialShapeSelection = [
            { shapePath: 'continent', shapeValue: 'Africa' },
            { shapePath: 'name', shapeValue: 'India' }
        ];
        this.selectionSettings = {
            enable: true,
            fill: 'green',
            border: { color: 'white', width: 2 }
        }
    }
}
```

 {% endtab %}

### Initial marker selection

Using the [`initialMarkerSelection`](../api/maps/initialMarkerSelectionSettingsModel), the marker shape can be selected initially. Markers render based on the [`latitude`](../api/maps/initialMarkerSelectionSettingsModel/#latitude) and [`longitude`](../api/maps/initialMarkerSelectionSettingsModel/#longitude) values.

**Note:** initialMarkerSelection is an Array property.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { Maps, Marker, Selection } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(Marker, Selection);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container'>
    <e-layers>
    <e-layer  [shapeData]= 'shapeData' [markerSettings] = 'markerSettings'></e-layer>
    </e-layers>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    public shapeData: object;
    public markerSettings: object;
    ngOnInit(): void {
        this.shapeData = world_map;
        this.markerSettings = [{
            visible: true,
            height: 20,
            width: 20,
            fill: 'green',
            shape:'Balloon',
            initialMarkerSelection: [{
               latitude: -6.64607562172573, longitude: -55.54687499999999
            }],
            selectionSettings: {
                enable: true,
                fill: 'blue',
                border: { color: 'white', width: 2}
            },
            dataSource: [
                { latitude: 49.95121990866204, longitude: 18.468749999999998, name:'Europe' },
                { latitude: 59.88893689676585, longitude: -109.3359375, name:'North America'},
                { latitude: -6.64607562172573, longitude: -55.54687499999999, name:'South America'}
            ]
        }];
    }
}
```

{% endtab %}

## Highlight

Each shape in the Maps can be highlighted during mouse hover on the Maps elements such as shapes, bubbles, markers and legends. Highlight is enabled by setting the [`enable`](../api/maps/highlightSettingsModel/#enable) property of [`highlightSettings`](../api/maps/highlightSettingsModel) to **true**.

The following properties are available to customize the highlight of Maps elements such as shapes, bubbles, markers and legends.

* [`border`](../api/maps/highlightSettingsModel/#border) - To customize the color, width and opacity of the border of which element is highlighted in Maps.
* [`fill`](../api/maps/highlightSettingsModel/#fill) - Applies the color for the element that is highlighted.
* [`opacity`](../api/maps/highlightSettingsModel/#opacity) - To customize the transparency for the element that is highlighted.

Hovering on the specific legend, the shapes which are bounded to the selected legend is also highlighted and vice versa.

<b>app.component.ts</b>

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { Maps, Highlight, Legend } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(Highlight, Legend);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' [legendSettings]='legendSettings'>
     <e-layers>
    <e-layer [shapeData] = 'shapeData' [shapePropertyPath]='shapePropertyPath' [shapeDataPath]='shapeDataPath' [dataSource]='dataSource' [shapeSettings]='shapeSettings' [highlightSettings] ='highlightSettings'></e-layer>
    </e-layers>
    </ejs-maps>`
})
export class AppComponent implements OnInit {
    public highlightSettings: object;
    public shapeData: object;
    public shapePropertyPath: string;
    public shapeDataPath: string;
    public dataSource: object;
    public shapeSettings: object;
    public legendSettings: object;
    ngOnInit(): void {
        this.highlightSettings = {
            enable: true,
            fill: 'green',
            border: { color: 'white', width: 2}
        }
        this.shapeData = world_map;
        this.shapePropertyPath= "name";
        this.shapeDataPath = "Country";
        this.dataSource = [
            {  "Country": "China", "Membership": "Permanent"},
            { "Country": "France","Membership": "Permanent" },
            { "Country": "Russia","Membership": "Permanent"},
            { "Country": "Kazakhstan","Membership": "Non-Permanent"},
            { "Country": "Poland","Membership": "Non-Permanent"},
            { "Country": "Sweden","Membership": "Non-Permanent"}
        ];
        this.shapeSettings = {
            colorValuePath: 'Membership',
                colorMapping: [
                    {
                        value: 'Permanent', color: '#D84444'
                    },
                    {
                        value: 'Non-Permanent', color: '#316DB5'
                   }]
        };
        this.legendSettings= {
            visible: true
        }
    }
}

```

{% endtab %}

### Enable highlight for bubbles

To enable the highlight for bubbles in Maps, set the [`highlightSettings`](../api/maps/highlightSettingsModel) in [`bubbleSettings`](../api/maps/bubbleSettingsModel) and set the [`enable`](../api/maps/highlightSettingsModel/#enable) property of [`highlightSettings`](../api/maps/highlightSettingsModel) as **true**.

>To use the bubble feature, the Bubble module must be injected.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { Maps, Bubble, Highlight } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(Bubble, Highlight);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container'>
    <e-layers>
    <e-layer  [shapeData]= 'shapeData' [bubbleSettings] = 'bubbleSettings'></e-layer>
    </e-layers>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    public shapeData: object;
    public shapeDataPath: object;
    public shapePropertyPath: object;
    public bubbleSettings: object;
    ngOnInit(): void {
        this.shapeData = world_map;
        this.shapeDataPath = 'name',
        this.shapePropertyPath = 'name',
        this.bubbleSettings = [{
            visible: true,
            dataSource: [
                { name: 'India', population: '38332521' },
                { name: 'South Africa', population: '19651127' },
                { name: 'Pakistan', population: '3090416' }
            ],
            highlightSettings: {
                enable: true,
                fill: 'green',
                border: { color: 'white', width: 2}
            },
            valuePath: 'population'
        }]
    }
}
```

{% endtab %}

### Enable highlight for markers

To enable the highlight for markers in Maps, set the [`highlightSettings`](../api/maps/highlightSettingsModel) in [`markerSettings`](../api/maps/markerSettingsModel) and set the [`enable`](../api/maps/highlightSettingsModel/#enable) property of [`highlightSettings`](../api/maps/highlightSettingsModel) as **true**.

**Note:** To use the marker feature, the Marker module must be injected.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { Maps, Marker, Highlight } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(Marker, Highlight);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container'>
    <e-layers>
    <e-layer  [shapeData]= 'shapeData' [markerSettings] = 'markerSettings'></e-layer>
    </e-layers>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    public shapeData: object;
     public markerSettings: object;
    ngOnInit(): void {
        this.shapeData = world_map;
        this.markerSettings = [{
           visible: true,
            height: 20,
            width: 20,
            fill: 'green',
            shape:'Balloon',
            highlightSettings: {
                enable: true,
                fill: 'blue',
                border: { color: 'white', width: 2}
            },
            dataSource: [
                { latitude: 49.95121990866204, longitude: 18.468749999999998, name:'Europe' },
                { latitude: 59.88893689676585, longitude: -109.3359375, name:'North America'},
                { latitude: -6.64607562172573, longitude: -55.54687499999999, name:'South America'}
            ]
        }];
    }
}
```

{% endtab %}

## Tooltip

On mouse over or touch end event, the tooltip is used to get more information about the layer, bubble, or marker. To enable tooltip in Maps, the **Tooltip** module must be injected into Maps using **Maps.Inject(Tooltip)** method. It can be enabled separately for layer or bubble or marker by using the [`visible`](../api/maps/tooltipSettingsModel/#visible) property of [`tooltipSettings`](../api/maps/tooltipSettingsModel/) as **true**. The [`valuePath`](../api/maps/tooltipSettingsModel/#valuepath) property in the tooltip takes the field name that presents in data source and displays that value as tooltip text. The [`tooltipDisplayMode`](../api/maps/mapsModel/#tooltipdisplaymode) property is used to change the display mode of the tooltip in Maps. Following display modes of tooltip are available in the Maps component. By default,  [`tooltipDisplayMode`](../api/maps/mapsModel/#tooltipdisplaymode) is set to **MouseMove**.

* MouseMove
* Click
* DoubleClick

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { Maps, MapsTooltip } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(MapsTooltip);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container'>
     <e-layers>
    <e-layer [shapeData] = 'shapeData' [tooltipSettings] ='tooltipSettings'></e-layer>
    </e-layers>
    </ejs-maps>`
})
export class AppComponent implements OnInit {
    public tooltipSettings: object;
    public shapeData: object;
    ngOnInit(): void {
        this.tooltipSettings ={
            visible: true,
            valuePath: 'name'
        }
        this.shapeData = world_map;
    }
}

```

{% endtab %}

**app.module.ts**
Injecting MapsTooltipService into NgModule.

```typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the MapsModule for the Maps component
import { MapsModule, MapsTooltipService} from '@syncfusion/ej2-angular-maps';
import { AppComponent }  from './app.component';

@NgModule({
  // declaration of ej2-angular-maps module into NgModule
  imports:      [ BrowserModule, MapsModule ],
  declarations: [ AppComponent ],
  providers: [MapsTooltipService],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

### Customization

The following properties are available to customize the tooltip of the Maps component.

* [`border`](../api/maps/tooltipSettingsModel/#border) - To customize the color, width and opacity of the border of the tooltip in layers, markers, and bubbles of Maps.
* [`fill`](../api/maps/tooltipSettingsModel/#fill) - Applies the color of the tooltip in layers, markers, and bubbles of Maps.
* [`format`](../api/maps/tooltipSettingsModel/#format) - To customize the format of the tooltip in layers, markers, and bubbles of Maps
* [`textStyle`](../api/maps/tooltipSettingsModel/#textstyle) - To customize the style of the text in the tooltip for layers, markers, and bubbles of Maps.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { Maps, MapsTooltip } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(MapsTooltip);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container'>
     <e-layers>
    <e-layer [shapeData] = 'shapeData' [tooltipSettings] ='tooltipSettings'></e-layer>
    </e-layers>
    </ejs-maps>`
})
export class AppComponent implements OnInit {
    public tooltipSettings: object;
    public shapeData: object;
    ngOnInit(): void {
        this.tooltipSettings ={
            visible: true,
            valuePath: 'name',
            fill: '#D0D0D0',
            textStyle: {
                color: 'green',
                fontFamily: 'Times New Roman',
                fontStyle: 'Sans-serif'
            }
        }
        this.shapeData = world_map;
    }
}

```

{% endtab %}

### Tooltip template

The HTML element can be rendered in the tooltip of the Maps using the [`template`](../api/maps/tooltipSettingsModel/#template) property of the [`tooltipSettings`](../api/maps/tooltipSettingsModel/).

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { Maps, MapsTooltip, ITooltipRenderEventArgs } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
import { default_data } from 'data.ts';
Maps.Inject(MapsTooltip);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container'>
    <e-layers>
   <e-layer [shapeData] ='shapeData' [shapePropertyPath]='shapePropertyPath' [shapeDataPath]='shapeDataPath' [dataSource]='dataSource' [shapeSettings]='shapeSettings' [tooltipSettings] ='tooltipSettings'></e-layer>
   </e-layers>
   </ejs-maps>`
})
export class AppComponent {
        public tooltipSettings: object ={
            visible: true,
            valuePath: 'continent',
            template: '<div style="width:60px; text-align:center; background-color: white; border: 2px solid black; padding-bottom: 10px;padding-top: 10px;padding-left: 10px;padding-right: 10px;"><span>${continent}</span></div>',
            textStyle: {
                color: 'black'
            }
        }
        public shapePropertyPath: string = "continent";
        public shapeDataPath: string = "continent";
        public dataSource: object = default_data;
        public shapeData: object = world_map;
}

```

{% endtab %}