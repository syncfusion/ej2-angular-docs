# Appearance

The appearance of the sparkline can be customized using margin, container Area border, and container Area background.

## Sparkline border

The `containerArea border` of the sparkline is used to render border to cover sparkline area.

The following code example shows the sparkline with overall border.

[`app.component.ts`]

{% tab template= "sparkline/getting-started/sparkline", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';
import { TooltipSettingsModel } from '@syncfusion/ej2-sparkline';

@Component({
    selector: 'app-container',
    template: `<ejs-sparkline id='container' width='350px' height='200px' [border]= 'border' [containerArea]='containerArea' [dataSource]="data" fill= '#b2cfff' type="Area">
    </ejs-sparkline>`
})
export class AppComponent {
    public data: object[] = [3, 6, 4, 1, 3, 2, 5];
    public containerArea: object= {
        border: { color: '#033e96', width: 2 }
    };
    public border: object= { color: '#033e96', width: 1 };
}

```

{% endtab %}

## Sparkline padding

Padding is used to specify padding value between container and sparkline. By default, padding value of the sparkline is 5. Sparkline `padding` values are specified by the left, right, top, and bottom.

The following code example shows the sparkline with overall padding is set to 20.

[`app.component.ts`]

{% tab template= "sparkline/getting-started/sparkline", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-sparkline id='container' width='350px' height='200px' [padding] = 'padding' [border]= 'border' [containerArea]='containerArea' [dataSource]="data" fill= '#b2cfff' type="Area">
    </ejs-sparkline>`
})
export class AppComponent {
    public data: object[] = [3, 6, 4, 1, 3, 2, 5];
    public containerArea: object= {
        border: { color: '#033e96', width: 2 }
    };
    public padding: object= { left: 20, right: 20, bottom: 20, top: 20};
    public border: object= { color: '#033e96', width: 1 };
}

```

{% endtab %}

## Sparkline area customization

The background color of the sparkline area can be customized using the `containerArea background` color. By default, the sparkline background color is `transparent`.

[`app.component.ts`]

{% tab template= "sparkline/getting-started/sparkline", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-sparkline id='container' width='350px' height='200px' [padding]= 'padding' [border]= 'border' [containerArea]='containerArea' [dataSource]="data" fill= '#b2cfff' type="Area">
    </ejs-sparkline>`
})
export class AppComponent {
    public data: object[] = [3, 6, 4, 1, 3, 2, 5];
    public containerArea: object= {
        border: { color: '#033e96', width: 2 },
        background: '#eff1f4',
    };
    public  padding: object= { left: 20, right: 20, bottom: 20, top: 20};
    public border: object= { color: '#033e96', width: 1 };
}

```

{% endtab %}

## Sparkline theme

Datalabel and track line colors of the sparkline will be changed based on theme. For example, for dark theme, the color of datalabel and track line should be white; for light theme, their value should be black. The possible values for sparkline theme are `Material`, `Fabric`, `Bootstrap`, and `Highcontrast`.

The following code example shows the color for datalabel and track line is set to white for dark theme.

[`app.component.ts`]

{% tab template= "sparkline/getting-started/sparkline", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';
import { TooltipSettingsModel } from '@syncfusion/ej2-sparkline';

@Component({
    selector: 'app-container',
    template: `<ejs-sparkline id='container' width='350px' height='200px' [axisSettings]= 'axisSettings' theme= 'Highcontrast' [dataLabelSettings]= 'dataLabelSettings' [tooltipSettings]= 'tooltipSettings' [border]= 'border'  [dataSource]="data" fill= '#007dd1' type="Line">
    </ejs-sparkline>`
})
export class AppComponent {
    public data: object[] = [3, 6, 4, 1, 3, 2, 5];
    public dataLabelSettings: object= { visible: ['All']};
    public tooltipSettings: object= {
        trackLineSettings: { visible: true }
    };
    public axisSettings: object= {
        minX: -1, maxX: 7
    };
   public border: object = { color: 'transparent', width: 2 };
}

```

{% endtab %}