# Markers

This section explains how to add markers to the sparkline.

## Adding marker to the sparkline

To add marker to the sparkline, specify the `visible` of `markerSettings` as following values. The `visible` will accept multiple values too.

* All - Enables markers for all points.
* Start - Enables marker for the start point.
* End - Enables marker for the end point.
* High - Enables marker for the high point.
* Low - Enables marker for the low point.
* Negative - Enables markers for the negative points.

The following code example shows enabling markers for all points.

[`app.component.ts`]

{% tab template= "sparkline/getting-started/sparkline", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-sparkline id='container' width='350px' height='200px' [markerSettings] ='markerSettings' [axisSettings] ='axisSettings'  [dataSource]="data" >
    </ejs-sparkline>`
})
export class AppComponent {
    public data: object[] = [0, 6, 4, 1, 3, 2, 5];
    public markerSettings: object= {
        visible: ['All']
    };
    public axisSettings: object ={
        minX: -1, maxX: 7, maxY: 7, minY: -1
    };
};
```

{% endtab %}

## Adding marker to special point

In sparkline, markers can be enabled for particular points such as the start, end, low, high, or negative. The following code examples shows enabling markers for the high and low points.

[`app.component.ts`]

{% tab template= "sparkline/getting-started/sparkline", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-sparkline id='container' width='350px' height='200px' [axisSettings]='axisSettings' [markerSettings]='markerSettings' lowPointColor= 'red' highPointColor= 'blue' [dataSource]="data" >
    </ejs-sparkline>`
})
export class AppComponent {
    public data: object[] = [3, 6, 4, 1, 3, 2, 5];
    public axisSettings: object ={
        minX: -1, maxX: 7, maxY: 7, minY: -1
    };
    public markerSettings: object ={
        visible: ['High', 'Low']
    };
};
```

{% endtab %}

## Customizing markers

Sparkline markers can be customized in terms of fill color, border color, width, opacity, and size. The following code example shows customizing marker's fill, border, and size.

[`app.component.ts`]

{% tab template= "sparkline/getting-started/sparkline", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-sparkline id='container' width='350px' height='200px' [axisSettings]='axisSettings' [markerSettings]='markerSettings' [dataSource]="data" >
    </ejs-sparkline>`
})
export class AppComponent {
    public data: object[] = [3, 6, 4, 1, 3, 2, 5];
    public markerSettings: object= {
        visible: ['All'],
        size: 5, fill: 'white', border: { color: 'blue', width: 2}
    };
    public axisSettings: object= {
        minX: -1, maxX: 7, maxY: 7, minY: -1
    };
};
```

{% endtab %}