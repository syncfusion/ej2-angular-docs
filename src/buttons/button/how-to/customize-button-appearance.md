---
title: "Customize Button Appearance"
component: "Button"
description: "Angular Button how to section, block button, repeat button, tooltip for Button, customization of button appearance, input and anchor elements."
---

# Customize Button Appearance

You can customize the appearance of the button by using the Cascading Style Sheets (CSS). Define the
CSS according to your requirement, and assign the class name to the [`cssClass`](../../api/button#cssclass) property.
In the following code snippet the background color, text color, height, width, and sharp corner
of the button can be customized through the `e-custom` class
for all states (hover, focus, and active).

{% tab template="button/howto", sourceFiles="app/**/*.ts,styles.css", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    styleUrls: ['styles.css'],
    template:  `<!-- To customize Button appearance. -->
                <!-- Refer the "e-custom" class details in "styles.css"-->
                <button ejs-button cssClass="e-custom">Custom</button>`
})

export class AppComponent { }
```

{% endtab %}