# State Persistence

## State Persistence

State persistence allows the Maps to retain the current modal value in the browser cookies for state maintenance. This action is handled through the `enablePersistence` property which is set to false by default. When it is set to true, some of the Maps component model values will be retained even after refreshing the page.

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps, Selection} from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(Selection);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' [enablePersistence] = 'enablePersistence' [zoomSettings] = 'zoomSettings'>
    <e-layers>
    <e-layer  [shapeData]= 'shapeData'></e-layer>
    </e-layers>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    ngOnInit(): void {
        public shapeData: Object = world_map;
        public enablePersistence = true;
         public zoomSettings: Object = {
            enable: true,
        };
   }
}
```