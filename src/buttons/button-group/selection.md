---
title: "ButtonGroup Selection and Nesting"
component: "ButtonGroup"
description: "ButtonGroup supports single selection, multiple selection, nesting with dropdownbutton and splitbutton components."
---

# Selection and Nesting

## Selection

### Single selection

ButtonGroup supports radio type selection in which only one button can be selected. This can be achieved by adding input element
along with `id` attribute with its corresponding label along with `for` attribute inside the target element. In this ButtonGroup,
the type of the input element should be `radio` and `e-btn` is added to the `label` element.

The following example illustrates the single selection behavior in ButtonGroup.

{% tab template="button-group/default", sourceFiles="app/**/*.ts", isDefaultActive=true  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<!-- To render ButtonGroup. -->
               <div class='e-btn-group'>
                    <input type="radio" id="radioleft" name="font" value="left"/>
                    <label class="e-btn" for="radioleft">Left</label>
                    <input type="radio" id="radiomiddle" name="font" value="middle"/>
                    <label class="e-btn" for="radiomiddle">Center</label>
                    <input type="radio" id="radioright" name="font" value="right"/>
                    <label class="e-btn" for="radioright">Right</label>
                </div>`
})

export class AppComponent { }
```

{% endtab %}

### Multiple selection

ButtonGroup supports checkbox type selection in which multiple button can be selected. This can be achieved by adding input element
along with `id` attribute with its corresponding label along with `for` attribute inside the target element. In this ButtonGroup,
the type of the input element should be `checkbox` and `e-btn` is added to the `label` element.

The following example illustrates the multiple selection behavior in ButtonGroup.

{% tab template="button-group/default", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<!-- To render ButtonGroup. -->
               <div class='e-btn-group'>
                    <input type="checkbox" id="check_bold" name="align" value="bold"/>
                    <label class="e-btn" for="check_bold">Bold</label>
                    <input type="checkbox" id="check_italic" name="align" value="italic"/>
                    <label class="e-btn" for="check_italic">Italic</label>
                    <input type="checkbox" id="check_underline" name="align" value="underline"/>
                    <label class="e-btn" for="check_underline">Underline</label>
                </div>`
})

export class AppComponent { }
```

{% endtab %}

## Nesting

Nesting with other components can be possible in ButtonGroup. The following components can be nested in ButtonGroup,
* DropDownButton
* SplitButton

For nesting support, [`SplitButton dependencies`](./../split-button/getting-started#dependencies) should be configured and added in
`system.config.js`.

### DropDownButton

To initialize DropDownButton component, refer [`DropDownButton Getting Started documentation`](./../drop-down-button/getting-started).

In the following example, the DropDownButton component is rendered in `app.component.ts` and `DropDownButtonModule` is imported in
`app.module.ts` file.

{% tab template="button-group/drop-down-button", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { ItemModel } from '@syncfusion/ej2-angular-splitbuttons';

@Component({
    selector: 'app-root',
    template: `<!-- To render ButtonGroup. -->
               <div class='e-btn-group'>
                    <button class='e-btn'>HTML</button>
                    <button class='e-btn'>CSS</button>
                    <button class='e-btn'>Javascript</button>
                    <button ejs-dropdownbutton [items]='items' content='More'></button>
                </div>`
})

export class AppComponent {
    private items: ItemModel[] = [
    {
        text: 'Learn SQL'
    },
    {
        text: 'Learn PHP'
    },
    {
        text: 'Learn Bootstrap'
    }];
 }
```

{% endtab %}

### SplitButton

To initialize SplitButton component refer [`SplitButton Getting Started documentation`](./../split-button/getting-started).

In the following example, the SplitButton component is rendered in `app.component.ts` and `SplitButtonModule` is imported in
`app.module.ts` file.

{% tab template="button-group/split-button", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { ItemModel } from '@syncfusion/ej2-angular-splitbuttons';

@Component({
    selector: 'app-root',
    template: `<!-- To render ButtonGroup. -->
               <div class='e-btn-group'>
                    <button class='e-btn'>Cut</button>
                    <button class='e-btn'>Copy</button>
                    <ejs-splitbutton content="Paste" [items]='items'></ejs-splitbutton>
                </div>`
})

export class AppComponent {
    private items: ItemModel[] = [
    {
        text: 'Paste'
    },
    {
        text: 'Paste Text'
    },
    {
        text: 'Paste Special'
    }];
 }
```

{% endtab %}

## See Also

* [Show ButtonGroup selected state on initial render](./how-to/show-buttongroup-selected-state-on-initial-render)
