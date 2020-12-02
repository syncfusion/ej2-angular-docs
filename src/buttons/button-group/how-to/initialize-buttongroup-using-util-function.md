---
title: "Initialize ButtonGroup using util function"
component: "ButtonGroup"
description: "ButtonGroup how to section, create ButtonGroup using util function, icons, form submit, show selected state on initial render."
---

# Initialize ButtonGroup using util function

Though, it is a CSS component for easy initialization of ButtonGroup `createButtonGroup` util function can be used.

To use `createButtonGroup` util function, [`SplitButton dependencies`](./../../split-button/getting-started#dependencies) should be
configured and it should be added in `system.config.js`.

Using `createButtonGroup` method, the Button options, selector, and cssClass is passed and the corresponding classes is added to the
elements.

## Create basic ButtonGroup

To create a basic ButtonGroup, the target element along with the button elements should be created and `createButtonGroup` should
be imported from `ej2-splitbuttons`.

## Create radio type ButtonGroup

To create a radio type ButtonGroup, the target element along with the input elements should be created with type `radio`.

## Create checkbox type ButtonGroup

Checkbox type ButtonGroup creation is similar to radio type ButtonGroup, instead the type of the input elements should be `checkbox`.

The following example illustrates how to create ButtonGroup using `createButtonGroup` function for basic, checkbox, and radio
type behaviors.

{% tab template="button-group/util", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';
import { createButtonGroup } from '@syncfusion/ej2-splitbuttons';

@Component({
    selector: 'app-root',
    template: `<!-- To render ButtonGroup. -->
               <h5>Normal behavior</h5>
               <div id='basic'>
                    <button></button>
                    <button></button>
                    <button></button>
                </div>
                <h5>Checkbox type behavior</h5>
                <div id='checkbox'>
                    <input type="checkbox" id="checkbold" name="font" value="bold" />
                    <input type="checkbox" id="checkitalic" name="font" value="italic" />
                    <input type="checkbox" id="checkundeline" name="font" value="underline" />
                </div>
                <h5>Radiobutton type behavior</h5>
                <div id='radio'>
                    <input type="radio" id="radioleft" name="align" value="left" />
                    <input type="radio" id="radiomiddle" name="align" value="middle" />
                    <input type="radio" id="radioright" name="align" value="right" />
                </div>`
})

export class AppComponent {

ngOnInit() {
createButtonGroup('#basic', {
    buttons: [
        { content: 'HTML' },
        { content: 'CSS' },
        { content: 'Javascript'}
    ]
});

createButtonGroup('#checkbox', {
    buttons: [
        { content: 'Bold' },
        { content: 'Italic' },
        { content: 'Undeline'}
    ]
});

createButtonGroup('#radio', {
    buttons: [
        { content: 'Left' },
        { content: 'Center' },
        { content: 'Right'}
    ]
});
}
}

```

{% endtab %}

> If null value is passed in button options, then that particular button will be skipped from processing in `createButtonGroup` util function.