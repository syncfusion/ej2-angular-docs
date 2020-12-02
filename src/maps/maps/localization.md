# Localization

Localization library allows to localize the default text content of Maps. In Maps component, it has the static text on some
features(like zooming toolbars) and this can be changed to any other culture(Arabic, Deutsch, French, etc) by defining
the locale value and translation object.

<!-- markdownlint-disable MD033 -->
<!-- markdownlint-disable MD010 -->

<table>
<tr>
<td><b>Locale key words</b></td>
<td><b>Text to display</b></td>
</tr>
<tr>
<td>Zoom</td>
<td>Zoom</td>
</tr>
<tr>
<td>ZoomIn</td>
<td>ZoomIn</td>
</tr>
<tr>
<td>ZoomOut</td>
<td>ZoomOut</td>
</tr>
<tr>
<td>Reset</td>
<td>Reset</td>
</tr>
<tr>
<td>Pan</td>
<td>Pan</td>
</tr>
<tr>
<td>ResetZoom</td>
<td>Reset Zoom</td>
</tr>
</table>

To load translation object in an application use load function of L10n class.

For more information about localization, refer this
[`localization`](http://ej2.syncfusion.com/documentation/base/localization.html)

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps } from '@syncfusion/ej2-maps';
import { world_map } from 'world-map.ts';
import { L10n } from '@syncfusion/ej2-base';

L10n.load({
    'ar-AR': {
        'maps': {
            ZoomIn: 'تكبير',
            ZoomOut: 'تصغير',
            Zoom: 'زوم',
            Pan: 'مقلاة',
            Reset: 'إعادة تعيين'
        },
    }
});

@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='container' [locale]="Locale" [zoomSettings]='zoom'>
    <e-layers>
    <e-layer [shapeData]="mapData"></e-layer>
    </e-layers>
    <ejs-maps>`
})

export class AppComponent implements OnInit {
    public mapData: object[] = world_map;
	public Locale: string = 'ar-AR';
    public zoom: object = {
     enable: true
    };
 ngOnInit(): void {
   }
}
```

{% endtab %}