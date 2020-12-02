# User Interactions

Options like zooming, panning, single click and double click, highlight and map selection enables the effective interaction on Map elements.

## Zooming

The zooming feature enables you to zoom in and out the Map to show in-depth information. It is controlled by
the `zoomFactor` property of the `zoomSettings` of the map. When the zoomFactor is increased, the Map is
zoomed in. When the zoomFactor is decreased, then the Map is zoomed out.

### Enable Zooming

To enable the zooming feature, set the `zoomSettings.enable` as true in maps. Zooming feature needs the
`ZoomService` injection to perform zooming actions, use module injection to inject ZoomService into Maps by using `NgModule providers`.

<!-- markdownlint-disable MD010 -->

### Enable panning

To enable the panning feature, set the [`enablePanning`](../api/maps/zoomSettings/#enablepanning) property of [`zoomSettings`](../api/maps/zoomSettings) to **true**.

[`app.component.ts`]

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
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
    ngOnInit(): void {
        public zoomSettings: Object = {
        enable: true,
		enablePanning: true
    };
    public shapeData: Object = world_map;
    }
}

```

{% endtab %}

[`app.module.ts`]
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

<b>Zooming toolbar</b>

By default, the toolbar is rendered with `zoom-in`, `zoom-out`, and `reset` options when it is set to 'true' in the `enable` property of `zoomSettings`. You can also customize the toolbar items using the `toolBArs` property in `zoomSettings`.

The following options are available in toolbar, and you can use the options as needed:

1. Zoom - Provides rectangular zoom support.
2. ZoomIn - Zooms in the maps.
3. ZoomOut - Zooms out the maps.
4. Pan - Switches to panning if rectangular zoom is activated.
5. Reset - Restores the maps to the default view.

Refer the [`API`](../api/maps/zoomSettingsModel) links for Zooming.

``` typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
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
    ngOnInit(): void {
        public zoomSettings: Object = {
        enable: true,
    };
    public shapeData: Object = world_map;
    }
}

```

<b>Pinch Zooming</b>

Use the `pinchZooming` property in `zoomSettings` to enable or disable the pinch zooming.

``` typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
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
    ngOnInit(): void {
        public zoomSettings: Object = {
        enable: true,
        pinchZooming:true
    };
    public shapeData: Object = world_map;
    }
}

```

<b>Single-click zooming</b>

Use the `zoomOnClick` property in `zoomSettings` to enable or disable the single-click zooming

``` typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
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
    ngOnInit(): void {
        public zoomSettings: Object = {
        enable: true,
        zoomOnClick:true
    };
    public shapeData: Object = world_map;
    }
}

```

<b>Double-click zooming</b>

Use the `doubleClickZoom` property in `zoomSettings` to enable or disable the double-click zooming.

``` typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
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
    ngOnInit(): void {
        public zoomSettings: Object = {
        enable: true,
        doubleClickZoom:true
    };
    public shapeData: Object = world_map;
    }
}

```

<b>Mouse wheel zooming</b>

Use the `mouseWheelZoom` property in `zoomSettings` to enable or disable mouse wheel zooming.

``` typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
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
    ngOnInit(): void {
        public zoomSettings: Object = {
        enable: true,
        mouseWheelZoom:true
    };
    public shapeData: Object = world_map;
    }
}

```

### Zooming with animation

You can use the `animationDuration` property in  `layers` property to zoom in or zoom out the maps with animation.

``` typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
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
    ngOnInit(): void {
        public zoomSettings: Object = {
        enable: true,
        mouseWheelZoom:true
    };
    pubic animationDuration: number = 500;
    public shapeData: Object = world_map;
    }
}

```

[`app.component.ts`]

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
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
    ngOnInit(): void {
        public zoomSettings: Object = {
        enable: true,
    };
    public shapeData: Object = world_map;
    }
}

```

{% endtab %}

[`app.module.ts`]
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

## Selection

Each shape in the Map can be selected and deselected during interaction with the shapes.

By tapping on the specific legend, the shapes which are bounded to the selected legend is also selected and vice versa.

The layer `selectionSettings.fill` property is used to change the selected layer shape color. The
`selectionSettings.border.color` and `selectionSettings.border.width` properties are used to customize the selected shape border.

You can select the shape by tapping the shape. The Single selection is enabled by the `selectionSettings.enable` property of shape layer.
When `selectionSettings.enable` is set to false, the shapes cannot be selected.

Refer the [`API`](../api/maps/selectionSettingsModel) and code snippet for Selection.

**Note:** Selection is separate module, need to inject it's service to work on Selection.

[`app.component.ts`]

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps, Selection } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(Selection);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' [zoomSettings] = 'zoomSettings'>
     <e-layers>
    <e-layer [shapeData] = 'shapeData' [selectionSettings] ='selectionSettings'></e-layer>
    </e-layers>
    </ejs-maps>`
})
export class AppComponent implements OnInit {
    ngOnInit(): void {
       public selectionSettings: Object = {
            enable: true,
            fill: 'green',
            border: { color: 'white', width: 2}
        };
    public shapeData: Object = world_map;
    }
}

```

{% endtab %}

[`app.module.ts`]
Injecting SelectionService into NgModule.

```typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the MapsModule for the Maps component
import { MapsModule, SelectionService} from '@syncfusion/ej2-angular-maps';
import { AppComponent }  from './app.component';

@NgModule({
  // declaration of ej2-angular-maps module into NgModule
  imports:      [ BrowserModule, MapsModule ],
  declarations: [ AppComponent ],
  providers: [SelectionService],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## Public method for the shape selection

Each shape in the map can be selected by calling the `shapeSelection` method. Input parameters for this method are layerIndex, propertyName, country name and selected value as in boolean state(true / false).

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
    <e-layer  [shapeData]= 'shapeData' [initialShapeSelection] = 'initialShapeSelection' [selectionSettings] ='selectionSettings'></e-layer>
    </e-layers>
    </ejs-maps> <button  id='select' (click)='select()'>select</button> <button id='unselect' (click)='unselect()'>unselect</button>`
})

export class AppComponent implements OnInit {
    @ViewChild('maps')
    public mapObj: MapsComponent;
    ngOnInit(): void {
        public shapeData: Object = world_map;
        public selectionSettings: Object = {
            enable: true,
            fill: 'green',
            border: { color: 'white', width: 2}
    };
    select(){
        this.mapObj.shapeSelection(0, "continent", "Asia", true);
    };
    unselect(){
        this.mapObj.shapeSelection(0, "continent", "Asia", false);
    }
   }
}
```

 {% endtab %}

## Initial shape selection

Initially, the shape can be selected by using the property `initialShapeSelection` and the values are mapped to the `shapePath` and `shapeValue`.

**Note:** initialShapeSelection is an Array property.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
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
    ngOnInit(): void {
         public shapeData: Object = world_map;
         public initialShapeSelection: Object = [
            { shapePath: 'continent', shapeValue: 'Africa' },
            { shapePath: 'name', shapeValue: 'India' }
        ];
        public selectionSettings: Object = {
            enable: true,
            fill: 'green',
            border: { color: 'white', width: 2}
    },
   }
}
```

 {% endtab %}

## Highlight

Each shape in the Map can be highlighted during mouse over on the shapes.

Hovering on the specific legend, the shapes which are bounded to the selected legend is also highlighted and vice versa.

The layer `highlightSettings.fill` property is used to change the highlighted layer shape color. The `highlightSettings.border.color` and
`highlightSettings.border.width` properties are used to customize the highlighted shape border.

You can highlight the shape by mouse over on the shape. The highlight is enabled by the `highlightSettings.enable` property of shape layer.
When `highlightSettings.enable` is set to false, the shapes cannot be highlighted.

**Note:** Highlight is separate module, need to inject to work on Highlight.

Refer the [`API`](../api/maps/highlightSettingsModel) and code snippet for Highlight.

[`app.component.ts`]

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps, Highlight } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(Highlight);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' [zoomSettings] = 'zoomSettings'>
     <e-layers>
    <e-layer [shapeData] = 'shapeData' [highlightSettings] ='highlightSettings'></e-layer>
    </e-layers>
    </ejs-maps>`
})
export class AppComponent implements OnInit {
    ngOnInit(): void {
      public highlightSettings: Object = {
            enable: true,
            fill: 'green',
            border: { color: 'white', width: 2}
        }
    public shapeData: Object = world_map;
    }
}

```

{% endtab %}

[`app.module.ts`]
Injecting HighlightService into NgModule.

```typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the MapsModule for the Maps component
import { MapsModule, HighlightService} from '@syncfusion/ej2-angular-maps';
import { AppComponent }  from './app.component';

@NgModule({
  // declaration of ej2-angular-maps module into NgModule
  imports:      [ BrowserModule, MapsModule ],
  declarations: [ AppComponent ],
  providers: [HighlightService],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## Tooltip

Tooltip used to get more information about layer or bubble or marker on mouse over or touch end event performing on that.
Tooltip is a separate module, So it needs module injection to work maps tooltip. Using NgModule provider you can inject MapsTooltipService.
tooltip module into maps.

Tooltip can be enabled separately for layer or bubble or marker by using `tooltipSettings.visible` as **true**.
Tooltip `valuePath` value need to set to display dataSource which field as tooltip text.
Below code snippet illustrate the tooltip enabled for layer to show shape data name field.

Refer the [`API`](../api/maps/tooltipSettingsModel) for Tooltip feature.

**Step: 1** Import the usmap geo json data from already created WorldMap.ts file and assign to `shapeData`.

**Step: 2** Import MapsTooltipService from `ej2-angular-maps` package and Inject to NgModule provider.

**Step: 3** Enable tooltip for layer using `tooltipSettings.visible` as true and bind `valuePath` value as 'name'.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps, MapsTooltip } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(MapsTooltip);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' [zoomSettings] = 'zoomSettings'>
     <e-layers>
    <e-layer [shapeData] = 'shapeData' [tooltipSettings] ='tooltipSettings'></e-layer>
    </e-layers>
    </ejs-maps>`
})
export class AppComponent implements OnInit {
    ngOnInit(): void {
      public tooltipSettings: Object ={
            visible: true,
            valuePath: 'name'
        }
    public shapeData: Object = world_map;
    }
}

```

{% endtab %}

[`app.module.ts`]
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
