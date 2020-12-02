# Localization

The sparkline control supports localization. The default culture for localization is `en-US`. You can change the culture using the `setCulture` method.

<!-- markdownlint-disable MD009 -->

## Tooltip format

Sparkline tooltip supports localization. The following code sample shows tooltip text with currency format based on culture.

[`app.component.ts`]

{% tab template= "sparkline/getting-started/sparkline", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';
import { TooltipSettingsModel } from '@syncfusion/ej2-sparkline';

@Component({
    selector: 'app-container',
    template: `<ejs-sparkline id='container' width='350px' height='200px' [containerArea]= 'containerArea' lineWidth= 3 format= 'c0' useGroupingSeparator= 'true' [padding]='padding' [dataSource]="data" fill= '#b2cfff' type="Area"
    [tooltipSettings]="tooltipSettings">
    </ejs-sparkline>`
})
export class AppComponent {
    public data: object[] = [30000, 60000, 40000, 10000, 30000, 20000, 50000];
    public containerArea: object= {
        border: { color: '#033e96', width: 2 }
    };
    public tooltipSettings: object= {
        visible: true
    };
    public padding: object = { left: 20, right: 20, bottom: 20, top: 20};
    public border: object = { color: '#033e96', width: 2 };
}

```

{% endtab %}

## Rtl

If you set the `enableRtl` property to true, then the sparkline will be rendered from rigt-to-left direction.

The following example shows the sparkline is render from "Right-to-left".

{% tab template= "sparkline/getting-started/sparkline", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';
import { TooltipSettingsModel } from '@syncfusion/ej2-sparkline';

@Component({
    selector: 'app-container',
    template: `<ejs-sparkline id='container' width='150px' height='150px'  [dataSource]="data" enableRtl= true
    >
    </ejs-sparkline>`
})
export class AppComponent {
    public data: object[] = [0, 6, 4, 1, 3, 2, 5];   
}

```

{% endtab %}