# Center position zooming

You can achieve the center position zooming by using the [centerPosition](../../api/maps#centerposition)
and [zoomFactor](../../api/maps/zoomSettings#zoomfactor) APIs as mentioned in the following code example. The
center position is used to configure the zoom level of maps, and zoom factor is used to specify the center
position where the map should be displayed.

[`app.module.ts`]

```typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent }  from './app.component';
import { MapsModule } from '@syncfusion/ej2-angular-maps';
import { ZoomService } from '@syncfusion/ej2-angular-maps';


@NgModule({
  imports:      [ BrowserModule,MapsModule ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ],
  providers:    [ ZoomService ]
})
export class AppModule { }

```

[`app.component.ts`]

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';
import { world_map } from 'world-map.ts';

@Component({
    selector: 'app-container',
    // specifies the template string for the maps component
    template:`<ejs-maps id='rn-container' [zoomSettings]='zoomSettings' [centerPosition]='centerPosition' style="display:block;">
    <e-layers>
    <e-layer [shapeData]='worldmap'></e-layer>
    </e-layers>
    </ejs-maps>`,
    encapsulation: ViewEncapsulation.None
  })
  export class AppComponent {
       public worldmap:object = world_map;
       public zoomSettings:object = {
          enable:false,
          zoomFactor:13
    };
    public centerPosition:object ={
        latitude: 25.54244147012483,
        longitude: -89.62646484375
    }
}
```

 {% endtab %}