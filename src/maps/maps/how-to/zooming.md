# Center position zooming

The center position zooming can be achieved by using the [`centerPosition`](../api/maps#centerposition) and [`zoomFactor`](../api/maps/zoomSettingsModel/#zoomfactor) properties as mentioned in the following example. The center position is used to configure the zoom level of Maps, and the zoom factor is used to specify the center position where the Maps should be displayed.

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
        enable:true,
        zoomFactor:13,
        maxZoom: 25
    };
    public centerPosition:object = {
        latitude: 25.54244147012483,
        longitude: -89.62646484375
    }
}
```

 {% endtab %}