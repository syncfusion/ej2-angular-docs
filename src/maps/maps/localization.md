---
title: " Localization in Angular Maps control | Syncfusion "

component: "Maps"

description: "Learn here all about Localization of Syncfusion Angular Maps control and more."
---

# Localization in Angular Maps

The localization library allows localizing the default text content of the Maps control. The Maps control has the static text of some features such as tooltip of zoom toolbar, and that can be changed to any other culture(Arabic, Deutsch, French, etc) by defining the locale value and translation object.

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
<td>Zoom In</td>
</tr>
<tr>
<td>ZoomOut</td>
<td>Zoom Out</td>
</tr>
<tr>
<td>Reset</td>
<td>Reset</td>
</tr>
<tr>
<td>Pan</td>
<td>Pan</td>
</tr>
</table>

To load translation object in the application, use `load` function of **L10n** class. For more information about localization, refer [here](http://ej2.syncfusion.com/documentation/base/localization.html).

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
    <e-layer [shapeData]="mapData" [tooltipSettings]='tooltipSettings'></e-layer>
    </e-layers>
    <ejs-maps>`
})

export class AppComponent implements OnInit {
    public mapData: object[] = world_map;
	public Locale: string = 'ar-AR';
    public zoom: object = {
        enable: true
    };
    public tooltipSettings: object = {
      enable: true
    };
 ngOnInit(): void {
   }
}
```

{% endtab %}