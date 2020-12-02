# Adding Multiple Layers in the Map

The multilayer support allows loading multiple shape files in a single container and enables maps to display more information.

Initialize the map component with SubLayer option by using the `type` property. The shape layer is the core
layer of the map. Multiple layers can be added in a shape layer as sublayers as mentioned in the following
code example. To know more about multiple layers, please refer to the [`API`](..
./api/maps/layerSettings)
documentation.

[`app.component.ts`]

{% tab template="maps/default-map/map", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';
import { world_map } from 'world-map.ts';
import { california } from 'california.ts';
import { texas } from 'texas.ts';

@Component({
    selector: 'app-container',
    // specifies the template string for the maps component
    template:`<div class="control-section">
    <div align='center'>
    <ejs-maps id='container' style="display:block;">
    <e-layers>
    <e-layer [shapeData]='usmap' [shapeSettings]='us_shapeSettings'></e-layer>
    <e-layer [shapeData]='texas' type='SubLayer' [shapeSettings]='texas_shapeSettings'></e-layer>
    <e-layer [shapeData]='california' type='SubLayer' [shapeSettings]='california_shapeSettings'></e-layer>
    </e-layers>
    </ejs-maps>
    </div>
    </div>`,
    encapsulation: ViewEncapsulation.None
  })
  export class AppComponent {
       public usmap=world_map;
       public us_shapeSettings = {
        fill: '#E5E5E5',
        border: {
            color: 'black',
            width: 0.1
        }
    };
    public texas=texas;
    public  texas_shapeSettings = {
        fill: 'rgba(141, 206, 255, 0.6)',
        border: {
            color: '#1a9cff',
            width: 0.25
        }
    };
    public california=california;
    public california_shapeSettings={
        fill: 'rgba(141, 206, 255, 0.6)',
        border: {
            color: '#1a9cff',
            width: 0.25
        }
    }
}
```

{% endtab %}