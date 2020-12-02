# Range Band

This section explains how to customize the sparkline with multiple range bands.

## Range band customization

The range band feature is used to highlight a particular range along with the y-axis using the [`startRange`] and [`endRange`] properties. You can also customize the [`color`] and [`opacity`] of the range band.

[`app.component.ts`]

{% tab template= "sparkline/getting-started/sparkline", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-sparkline id='container' width='150px' height='150px' lineWidth= 2 fill = '#0d3c9b' [rangeBandSettings] = 'rangeBandSettings' [dataSource]="data">
    </ejs-sparkline>`
})
export class AppComponent {
    public data: object[] = [ 0, 6, 4, 1, 3, 2, 5 ];
    public rangeBandSettings: object[] = [{
        startRange: 1,
        endRange: 3,
        color: '#bfd4fc',
        opacity:0.4
        }];
};
```

{% endtab %}

## Multiple range band customization

You can define multiple range bands to a sparkline as shown in the following code sample.

[`app.component.ts`]

{% tab template= "sparkline/getting-started/sparkline", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-sparkline id='container' width='150px' height='150px' lineWidth= 2 fill= '#0d3c9b' [rangeBandSettings] ='rangeBandSettings' [dataSource]="data" >
    </ejs-sparkline>`
})
export class AppComponent {
    public data: object[] = [0, 6, 4, 1, 3, 2, 5];
    public rangeBandSettings: object[] = [
            {
                startRange: 1,
                endRange: 2,
                color: '#bfd4fc',
                opacity:0.4
            },
            {
                startRange: 4,
                endRange: 5,
                color: 'red',
                opacity:0.4
            }
        ]
};
```

{% endtab %}