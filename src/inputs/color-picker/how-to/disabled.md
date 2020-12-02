# Disabled

To achieve disabled state in ColorPicker, set the [`disabled`](../../api/color-picker#disabled) property to `true`. The ColorPicker pop-up cannot be accessed in disabled state.

The following example shows the `disabled` state of ColorPicker component.

{% tab template="colorpicker/how-to", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<h4>Disabled State</h4>
               <!-- To disable ColorPicker. -->
               <input ejs-colorpicker type="color" id="element" [disabled]="true" />`
})

export class AppComponent { }
```

{% endtab %}