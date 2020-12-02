# Hide control buttons

ColorPicker can be rendered without control buttons (Apply/Cancel). In this case, while selecting a color, the
ColorPicker pop-up is closed and selected colors will be applied directly. To hide control buttons, set the [`showButtons`](../../api/color-picker#showbuttons) property to `false`.

{% tab template="colorpicker/how-to", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<h4>Choose Color</h4>
               <!-- To hide control buttons. -->
               <input ejs-colorpicker type="color" id="element" [showButtons]="false" />`
})

export class AppComponent { }
```

{% endtab %}
