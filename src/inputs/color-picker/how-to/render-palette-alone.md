# Render palette alone

To render the `Palette` alone in ColorPicker, specify the [`mode`](../../api/color-picker#mode) property as `Palette`, and set the [`modeSwitcher`](../../api/color-picker#modeswitcher) property to `false`.

In the following sample, the [`showButtons`](../../api/color-picker#showbuttons) property is disabled to hide the control buttons and it renders only the `Palette` area.

{% tab template="colorpicker/how-to", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<h4>Select Color</h4>
               <!-- To render Picker. -->
               <input ejs-colorpicker type="color" id="element" mode="Palette" [modeSwitcher]="false" [showButtons]="false" />`
})

export class AppComponent { }
```

{% endtab %}

>> To render `Picker` alone specify the [`mode`](../../api/color-picker#mode) property as 'Picker'.
