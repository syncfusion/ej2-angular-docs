# Two way binding

ColorPicker component supports two-way property binding.

The steps to perform two-way binding.

* Create [ColorPicker](https://ej2.syncfusion.com/angular/documentation/color-picker/getting-started#getting-started)
component and binds the [`value`](../../api/color-picker#value) property as like the below code snippet.

```html

<input ejs-colorpicker type="color" class="form-control" id="colorpicker" required [(value)]="value" name="colorpicker" />

```

* Create text box and bind the value using ngModel.

```html

<input type="text" id="name" name="name" class="form-control" [(ngModel)]="value" />

```

* And name the same variable name in both color picker and text box. Which will help to view
the two-way binding i.e. changing value in color picker will change the textbox value and vice versa.

* Initialize the value of the variable in component file, while will be bound to color picker and text
box initially. The values will be changed synchronously while changing any one (color picker or text-box) value.

{% tab template="colorpicker/ng-model", sourceFiles="app/**/*", isDefaultActive=true %}

```typescript
import { Component, Input } from '@angular/core';
import { FormGroup } from '@angular/forms';
import { Browser } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    templateUrl: 'app/template.html',
    styleUrls:['index.css']
})

export class AppComponent {
    private cValue: string = "#1de4d7";

    get value(): string {
        if (Browser.info.name === 'msie' && this.cValue.length > 7) {
            return this.cValue.substring(0, this.cValue.length - 2);
        } else {
            return this.cValue;
        }
    }

    @Input('value')
    set value(value: string) {
        this.cValue = value;
    }
}
```

{% endtab %}

>> By default, the selected color value returns 8 digit hex code in [`value`](../../api/color-picker#value) property. Some browser like IE won't support the 8 digit hex code. In such case, you can use getter setter method to change the value to supported format as like the above sample.
