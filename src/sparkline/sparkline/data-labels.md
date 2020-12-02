# Data Labels

Data labels are used to display values of data points to improve the readability.

## Enable data label

To enable data label for sparkline series, provide `visible` of the `dataLabelSettings` as following possible values:

* All - Enables data label of  all points.
* Start - Enables data label of the start point.
* End - Enables data label of the end point.
* High - Enables data label of the high point.
* Low - Enables data label of the low point.
* Negative - Enables data labels of the negative points.

The following example shows enabling sparkline data label for all points.

[`app.component.ts`]

{% tab template= "sparkline/getting-started/sparkline", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-sparkline id='container' width='350px' height='200px' fill= 'blue' [axisSettings] = 'axisSettings' [dataLabelSettings] = 'dataLabelSettings' [dataSource]="data" >
    </ejs-sparkline>`
})
export class AppComponent {
    public data: object[] = [0, 6, 4, 1, 3, 2, 5];
    public axisSettings: object ={
        minX: -1, maxX: 7, maxY: 7, minY: -1
    };
    public dataLabelSettings: object ={
        visible: ['All']
    },
};
```

{% endtab %}

## Customize data label

Data labels can be customized using the fill, border, opacity, and textStyle. The following code example shows customizing data label border, text color, and fill color.

[`app.component.ts`]

{% tab template= "sparkline/getting-started/sparkline", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-sparkline id='container' width='350px' height='200px' [dataLabelSettings]='dataLabelSettings' [axisSettings] = 'axisSettings' fill= 'blue'[dataSource]="data" >
    </ejs-sparkline>`
})
export class AppComponent {
    public data: object[] = [0, 6, 4, 1, 3, 2, 5];
    public axisSettings: object ={
        minX: -1, maxX: 7, maxY: 8, minY: -1
    };
    // To customize data label fill, border, and text color
    public dataLabelSettings: object = {
        visible: ['All'],
        border: { color: 'blue', width: 1},
        fill: 'blue', opacity: 0.4,
        textStyle: {
            color: 'white'
        }
    };
};
```

{% endtab %}

## Format data label text

The text of data labels can be formatted using the `format` API in the sparkline `dataLabelSettings`. By default, data label shows the y-value of point. The following code example shows how to display x and y-values for points.

[`app.component.ts`]

{% tab template= "sparkline/getting-started/sparkline", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-sparkline id='container' width='500px' height='200px' [axisSettings]='axisSettings' fill= 'blue' [dataLabelSettings]='dataLabelSettings' valueType= 'Category' [dataSource]="data"  xName= 'x' yName= 'y'>
    </ejs-sparkline>`
})
export class AppComponent {
    public data: object[] = [{x: 'Mon', y: 3 },{x: 'Tue', y: 5 },{x: 'Wed', y: 2 },{x: 'Thu', y: 4 },{x: 'Fri', y: 6 },];
    public dataLabelSettings: object = {
        format: '${x} : ${y}'
        visible: ['All'],
        border: { color: 'blue', width: 1},
        fill: 'blue', opacity: 0.4,
        textStyle: {
            color: 'white'
        }
    };
    public axisSettings: object = {
        minX: -1, maxX: 7, maxY: 8, minY: -1
    },
};
```

{% endtab %}
