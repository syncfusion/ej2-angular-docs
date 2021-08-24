# State Persistence

## State Persistence

For state maintenance, state persistence allows Maps to save the current modal value in browser cookies. This action is handled through the [`enablePersistence`](../api/maps#enablepersistence) property which is set to **false** by default. When this property is set to true, some of the Maps component model values are preserved even after the page is refreshed.

```typescript
import { Component, OnInit } from '@angular/core';
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
    public shapeData: object;
    public zoomSettings: object;
    public enablePersistence: boolean;
    ngOnInit(): void {
        this.shapeData = world_map;
        this.enablePersistence = true;
        this.zoomSettings = {
            enable: true,
        };
    }
}
```