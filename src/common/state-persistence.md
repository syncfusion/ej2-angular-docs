# State Persistence

Syncfusion Angular UI Components has support for persisting component’s state across page refreshes or
navigation. To enable this feature, set `enablePersistence` property as true to the required component.
This will store the component’s state in the browser’s `localStorage` object on page `unload` event. For
example, we have enabled persistence to grid component in the following code.

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    template: `<ejs-grid #grid [dataSource]='data' [allowPaging]='true' [allowFiltering]='true'
    [enablePersistence]='true' height='210px'>
                <e-columns>
                    <e-column field='OrderID' headerText='Order ID' textAlign='right' width=120></e-column>
                    <e-column field='CustomerID' headerText='Customer ID' width=150></e-column>
                    <e-column field='ShipCity' headerText='Ship City' width=150></e-column>
                    <e-column field='ShipName' headerText='Ship Name' width=150></e-column>
                </e-columns>
                </ejs-grid>`,
})
export class AppComponent implements OnInit {

    public data: Object[];
    @ViewChild('grid')
    public grid: GridComponent;

    ngOnInit(): void {
        this.data = data;
    }
}
```