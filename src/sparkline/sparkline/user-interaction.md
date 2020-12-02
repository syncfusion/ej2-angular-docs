# User interactions

Sparkline has two user interaction features: tooltip and tracker line.

## Tooltip

The sparkline provides options to display details about values of data points through tooltips when hovering the mouse over data point. To use tooltip in sparkline, inject the `SparklineTooltip` module to sparkline using the inject method.

The following code example shows enabling tooltip for sparkline with format.

[`app.component.ts`]

{% tab template= "sparkline/getting-started/sparkline", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { TooltipSettingsModel } from '@syncfusion/ej2-sparkline';

@Component({
    selector: 'app-container',
    template: `<ejs-sparkline id='container' width='500px' height='200px' [axisSettings]='axisSettings' [tooltipSettings]='tooltipSettings'  fill= 'blue'valueType= 'Category' [dataSource]="data" xName="x" yName="y">
    </ejs-sparkline>`
})
export class AppComponent {
    public data: object[] = [{x: 'Mon', y: 3 },{x: 'Tue', y: 5 },{x: 'Wed', y: 2 },{x: 'Thu', y: 4 },{x: 'Fri', y: 6 }];
    public axisSettings: object ={
        minX: -1, maxX: 7, maxY: 8, minY: -1
    };
    public tooltipSettings: object = {
        visible: true,
        // formatting tooltip text
        format: '${x} : ${y}'
    };
};
```

{% endtab %}

### Tooltip customization

The fill color, text styles, format, and border of the tooltip can be customized. The following code example shows customization of tooltip's fill color and text style.

[`app.component.ts`]

{% tab template= "sparkline/getting-started/sparkline", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { TooltipSettingsModel } from '@syncfusion/ej2-sparkline';


@Component({
    selector: 'app-container',
    template: `<ejs-sparkline id='container' width='500px' height='200px' [axisSettings]='axisSettings' [tooltipSettings]='tooltipSettings'  fill= '#033e96' valueType= 'Category' [dataSource]="data" xName="x" yName="y">
    </ejs-sparkline>`
})
export class AppComponent {
    public data: object[] = [{x: 'Mon', y: 3 },{x: 'Tue', y: 5 },{x: 'Wed', y: 2 },{x: 'Thu', y: 4 },{x: 'Fri', y: 6 }];
    public axisSettings: object ={
        minX: -1, maxX: 7, maxY: 8, minY: -1
    };
    public tooltipSettings: object= {
        visible: true,
        format: '${x} : ${y}',
        fill: '#033e96',
        textStyle: {
            color: 'white'
        },
    }
};
```

{% endtab %}

### Tooltip template

Sparkline tooltip has template support. By using tooltip template, you can customize tooltips. The following code example shows more customization options provided to  `sparktooltip` css class that is used in tooltip template div. Using this template, images also can be added to tooltip.

```css
.sparktooltip {
  border-radius: 5px;
  background: #008cff;
  color: #FFFFFF !important;
  font-size: 16px;
  font-style: italic;
  padding: 8px;
}
```

[`app.component.ts`]

{% tab template= "sparkline/getting-started/sparkline", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { TooltipSettingsModel } from '@syncfusion/ej2-sparkline';


@Component({
    selector: 'app-container',
    template: `<ejs-sparkline id='container' width='500px' height='200px' [axisSettings]='axisSettings' [tooltipSettings]='tooltipSettings'  fill= '#033e96' valueType= 'Category' [dataSource]="data" xName="x" yName="y">
    </ejs-sparkline>`
})
export class AppComponent {
    public data: object[] = [{x: 'Mon', y: 3 },{x: 'Tue', y: 5 },{x: 'Wed', y: 2 },{x: 'Thu', y: 4 },{x: 'Fri', y: 6 }];
    public axisSettings: object ={
        minX: -1, maxX: 7, maxY: 8, minY: -1
    };
    public tooltipSettings: object= {
        visible: true,
        template: '<div style=" border-radius: 5px; background: #008cff; padding: 8px; color: #FFFFFF !important; font-size: 16px; font-style: italic;">${x} : ${y}<div>'
    }
};
```

{% endtab %}

## Track line

The track line tracks data points that are closer to the mouse position or touch contact.

To enable track lines for sparkline, specify the `visible` option of  `trackLineSettings` to true. Based on theme, tracker color will be changed. The default value of tracker color is black.

To use track line in sparkline, inject the `SparklineTooltip` module to sparkline using the inject method.

[`app.component.ts`]

{% tab template= "sparkline/getting-started/sparkline", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { TooltipSettingsModel } from '@syncfusion/ej2-sparkline';

@Component({
    selector: 'app-container',
    template: `<ejs-sparkline id='container'width='500px' height='200px' [axisSettings]='axisSettings' [tooltipSettings]='tooltipSettings'  fill= '#033e96' valueType= 'Category' [dataSource]="data" xName="x" yName="y">
    </ejs-sparkline>`
})
export class AppComponent { public data: object[] = [{x: 'Mon', y: 3 },{x: 'Tue', y: 5 },{x: 'Wed', y: 2 },{x: 'Thu', y: 4 },{x: 'Fri', y: 6 }];
public axisSettings: object ={
        minX: -1, maxX: 7, maxY: 8, minY: -1
    };
    public tooltipSettings: object= {
        visible: true,
        trackLineSettings: {
            visible: true,
            color: '#033e96',
            width: 1
        }
        };
};
```

{% endtab %}