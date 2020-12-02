---
title: "ButtonGroup Types and Styles"
component: "ButtonGroup"
description: "ButtonGroup CSS component supports outline type and predefined styles."
---

# Types and Styles

This section explains about different types and styles of ButtonGroup.

## ButtonGroup types

### Outline ButtonGroup

An Outline ButtonGroup has a border with transparent background. To create Outline ButtonGroup, `e-outline` class should
be added to the target element and to each button elements using `cssClass` property.

The following sample illustrates how to achieve an Outline ButtonGroup,

{% tab template="button-group/default", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<!-- To render ButtonGroup. -->
               <div class='e-btn-group e-outline'>
                  <button ejs-button cssClass='e-outline'>HTML</button>
                  <button ejs-button cssClass='e-outline'>CSS</button>
                  <button ejs-button cssClass='e-outline'>Javascript</button>
                </div>`
})

export class AppComponent { }
```

{% endtab %}

> ButtonGroup does not have support for `flat` and `round` types.

## ButtonGroup styles

The Essential JS 2 ButtonGroup has the following predefined styles. This can be achieved by adding corresponding class name
in each button elements using `cssClass` property.

| Class | Description |
| -------- | -------- |
| e-primary | Used to represent a primary action. |
| e-success | Used to represent a positive action. |
| e-info | Used to represent an informative action. |
| e-warning | Used to represent an action with caution. |
| e-danger | Used to represent a negative action. |

The following example illustrates how to achieve predefined styles in ButtonGroup.

{% tab template="button-group/default", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<!-- To render ButtonGroup. -->
               <div class='e-btn-group'>
                 <button ejs-button cssClass='e-info'>View</button>
                 <button ejs-button>Edit</button>
                 <button ejs-button cssClass='e-danger'>Delete</button>
               </div>`
})

export class AppComponent { }
```

{% endtab %}

> Predefined ButtonGroup styles provide only the visual indication. So,
ButtonGroup content should define the ButtonGroup style for the users of assistive technologies such as screen readers.

## See Also

* [ButtonGroup with icons](./how-to/create-buttongroup-with-icons)
* [Create ButtonGroup with rounded corner](./how-to/create-buttongroup-with-rounded-corner)