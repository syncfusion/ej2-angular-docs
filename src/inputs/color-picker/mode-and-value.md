# Mode and Value

## Rendering palette at initial load

By default, the `Picker` area will be rendered at initial load. To render the Palette area while opening the ColorPicker pop-up, and specify the [`mode`](../api/color-picker#mode) property as `Palette`.

In the following sample, it will render the `Palette` at initial load.

{% tab template="colorpicker/getting-started/default", isDefaultActive=true, sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<h4>Select Color</h4>
               <input ejs-colorpicker type="color" id="element" mode="Palette" />`
})

export class AppComponent { }
```

{% endtab %}

## Color value

The [`value`](../api/color-picker#value) property can be used to specify the color value to the
ColorPicker. It supports either `three` or `six` digit hex codes. To include `opacity`, set the color value as `four` or `eight` digit hex code.

In the following sample, the color value sets as `four` digit hex code, the last digit represents the `opacity` value.

{% tab template="colorpicker/value", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<h4>Choose Color</h4>
               <!-- To set color value. -->
               <input ejs-colorpicker type="color" id="element" value="035a" />`
})

export class AppComponent { }
```

{% endtab %}

>> The [`value`](../api/color-picker#value) property supports hex code with or without `#` prefix.

## See Also

* [How to render palette alone](./how-to/render-palette-alone)
* [Custom palette](./how-to/customize-colorpicker#custom-palette)
* [No color support in palette](./how-to/handle-no-color-support)
