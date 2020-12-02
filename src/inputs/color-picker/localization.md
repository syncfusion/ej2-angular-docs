# Localization and RTL

## Localization

The `Localization` library allows you to localize default text content of the
ColorPicker. The ColorPicker component has static text for `control buttons (apply / cancel)` and `mode switcher` that can be changed to other cultures (Arabic, Deutsch, French, etc.) by defining the
[`locale`](../api/color-picker#locale) value and translation object.

The following list of properties and its values are used in the ColorPicker.

Locale key words |Text
-----|-----
Apply |Apply
Cancel |Cancel
ModeSwitcher |Switch Mode

### Loading translations

To load translation object in an application use `load` function of `L10n` class.

The below example demonstrates the ColorPicker in `Deutsch` culture.

{% tab template="colorpicker/how-to", isDefaultActive=true, sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { L10n } from '@syncfusion/ej2-base';

L10n.load({
    'de-DE': {
        'colorpicker': {
            'Apply': 'Anwenden',
            'Cancel': 'Abbrechen',
            'ModeSwitcher': 'Modus wechseln'
        }
    }
});

@Component({
    selector: 'app-root',
    template: `<h4>Choose Color</h4>
               <input ejs-colorpicker type="color" id="element" locale="de-DE" />`
})

export class AppComponent { }
```

{% endtab %}

## Right to Left - RTL

ColorPicker component has `RTL` support. It helps to render the ColorPicker from right-to-left direction.
It improves the user experiences and accessibility for users who use right-to-left languages(Arabic, Farsi, Urdu, etc). This can be achieved by setting the [`enableRtl`](../api/color-picker#enablertl) property to `true`.

The following example illustrates how to enable right-to-left support in ColorPicker component.

{% tab template="colorpicker/how-to", isDefaultActive=true, sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { L10n } from '@syncfusion/ej2-base';

L10n.load({
    'ar-AE': {
        'colorpicker': {
            'Apply': 'تطبيق',
            'Cancel': 'إلغاء',
            'ModeSwitcher': 'مفتاح كهربائي الوضع'
        }
    }
});

@Component({
    selector: 'app-root',
    template: `<h4>Choose Color</h4>
               <input ejs-colorpicker type="color" id="element" [enableRtl]="true" locale="ar-AE" />`
})

export class AppComponent { }
```

{% endtab %}

## See Also

* [More information about localization](./../common/localization)