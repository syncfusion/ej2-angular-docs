
# User Interaction

<!-- markdownlint-disable MD036 -->

## Tooltip

<!-- markdownlint-disable MD036 -->

Linear gauge will display the details about the pointer value through tooltip, when the mouse is moved over the pointer.

**Enable Tooltip for Pointer**

By default, tooltip is not visible. Enable the tooltip by setting
[`enable`](../api/linear-gauge/tooltipSettingsModel/#enable-boolean) property to true and by injecting `GaugeTooltipService` module into the `@NgModule.providers`.

{% tab template= "linear-gauge/user-interaction", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container" [tooltip]='Tooltip'>
        <e-axes>
            <e-axis>
             <e-pointers>
               <e-pointer value=80></e-pointer>
             </e-pointers>
            </e-axis>
        </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent implements OnInit {
    public Tooltip:Object;
    ngOnInit(): void {
        this.Tooltip = {
            enable: true
        };
    }
}
```

{% endtab %}

<!-- markdownlint-disable MD013 -->

**Format the Tooltip**

<!-- markdownlint-disable MD013 -->

By default, tooltip will show the information of pointer value only. In addition to that, you can show more information in tooltip. For example, the format `${value}` shows pointer value with currency symbol.

{% tab template= "linear-gauge/user-interaction", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container" [tooltip]='Tooltip'>
        <e-axes>
            <e-axis>
            <e-pointers>
               <e-pointer value=80></e-pointer>
             </e-pointers>
            </e-axis>
        </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent implements OnInit {
    public Tooltip:Object;
    ngOnInit(): void {
        this.Tooltip = {
             enable: true,
             format: '${value}'
        };
    }
}
```

{% endtab %}

**Tooltip Template**

Any HTML elements can be displayed in the tooltip by using the ‘template’ property of the tooltip. You can use the {value} as place holders in the HTML element to display the pointer values of the corresponding axis.

{% tab template= "linear-gauge/user-interaction", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container" [tooltip]='Tooltip'>
        <e-axes>
            <e-axis>
            <e-pointers>
               <e-pointer value=80></e-pointer>
             </e-pointers>
            </e-axis>
        </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent implements OnInit {
    public Tooltip:Object;
    ngOnInit(): void {
        this.Tooltip = {
            enable: true,
            //tooltip template for Linear gauge
            template: '<div>Pointer: 80 </div>'
        };
    }
}
```

{% endtab %}

**Customize the Appearance of Tooltip**

* [`fill`](../api/linear-gauge/tooltipSettings/#fill-string) - Specifies fill color for tooltip
* [`border`](../api/linear-gauge/tooltipSettings/#border-bordermodel) - Specifies tooltip border width and color
* [`textStyle`](../api/linear-gauge/tooltipSettings/#textstyle-fontmodel) - Specifies the tooltip text style, such as color, font family, font style and font weight

{% tab template= "linear-gauge/user-interaction", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container" [tooltip]='Tooltip'>
        <e-axes>
            <e-axis>
            <e-pointers>
               <e-pointer value=80></e-pointer>
             </e-pointers>
            </e-axis>
        </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent implements OnInit {
    public Tooltip:Object;
    ngOnInit(): void {
        this.Tooltip = {
            enable: true,
            fill: '#e5bcbc',
            border: {
                color: '#d80000',
                width: 2
            }
        };
    }
}
```

{% endtab %}

## Pointer Drag

You can drag and drop either marker or bar pointer over the desired axis value using [`enableDrag`](../api/linear-gauge/pointer/#enabledrag-boolean) property in the [`pointer`](../api/linear-gauge/pointer/#pointer-pointermodel).

{% tab template= "linear-gauge/user-interaction", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-lineargauge id="gauge-container" height='350'>
        <e-axes>
            <e-axis>
            <e-pointers>
               <e-pointer value=80 enableDrag=true></e-pointer>
             </e-pointers>
            </e-axis>
        </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent implements OnInit {
    ngOnInit(): void {
    }
}
```

{% endtab %}