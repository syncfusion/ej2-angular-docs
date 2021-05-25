---
title: "Toolbar Item configuration"
component: "Toolbar"
description: "Toolbar items are constructed with built-in command types or item templates such as separator, button, and input."
---

# Item Configuration

The Toolbar can be rendered by defining an array of [`items`](../api/toolbar#items). Items can be constructed with the following built-in command types or item template.

## Button

`Button` is the default command [`type`](../api/toolbar/item#type), and it can be rendered by using the [`text`](../api/toolbar/item#text) property.
Properties of the button command type:

  Property   | Description
------------ | -------------
  [`text`](../api/toolbar/item#text) | The text to be displayed for button.
 [`id`](../api/toolbar/item#id) | The ID of the button to be rendered. If the ID is not given, auto ID is generated.
  [`prefixIcon`](../api/toolbar/item#prefixicon) | Defines the class used to specify an icon for the button. The icon is `positioned before` the text if text is available or the icon alone button is rendered.
[`suffixIcon`](../api/toolbar/item#suffixicon) | Defines the class used to specify an icon for the button. The icon is `positioned after` the text if text is available. If both [`prefixIcon`](../api/toolbar/item#prefixicon) and [`suffixIcon`](../api/toolbar/item#suffixicon) are specified, only `prefixIcon` is considered.
  [`width`](../api/toolbar/item#width) | Used to set the [`width`](../api/toolbar/item#width) of the button.
  [`align`](../api/toolbar/item#align) | Specifies the location for aligning Toolbar items.

## Separator

The `Separator` type adds a vertical separation between the Toolbar's single/multiple commands.

{% tab template="toolbar/toolbar-items", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { ToolbarComponent } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-container',
    template: `
        <ejs-toolbar>
          <e-items>
             <e-item text='Cut'></e-item>
             <e-item text='Copy'></e-item>
             <e-item type='Separator'></e-item>
             <e-item text='Paste'></e-item>
             <e-item type='Separator'></e-item>
             <e-item text='Undo'></e-item>
             <e-item text='Redo'></e-item>
          </e-items>
        </ejs-toolbar>
        `
})

export class AppComponent {

}
```

{% endtab %}

> If `Separator` is added as first or last item, it is not visible.

## Input

The `Input` type is only applicable for adding `template` elements when the [`template`](../api/toolbar/item#template) property is defined as an `object`.
Input type creates an `input element` internally that acts as the container for `Syncfusion` input based components.

### NumericTextBox

* The `NumericTextBox` component can be included by importing the `NumericTextBox` module from `ej2-inputs`.

* Initialize the `NumericTextBox` in template property, in which the Toolbar item type set as `Input`.

* Related `NumericTextBox` component properties are also can be configured like as below.

```javascript
new NumericTextBox( { format: 'c2' }))
```

### DropDownList

* The `DropDownList` component can be included by importing the `DropDownList` module from `ej2-dropdowns`.

* Initialize the `DropDownList` in template property, in which the Toolbar item type set as `Input`.

* Related `DropDownList` component properties are also can be configured like as below.

```javascript
new DropDownList({ width:100 })
```

### CheckBox

* The `CheckBox` component can be included by importing the `CheckBox` module from `ej2-buttons`.

* Initialize the `CheckBox` in template property, in which the Toolbar item type set as `Input`.

* Related `CheckBox` component properties are also can be configured like as below.

```javascript
new CheckBox({ label: 'Checkbox', checked: true })
```

### RadioButton

* The `RadioButton` component can be included by importing the `RadioButton` module from `ej2-buttons`.

* Initialize the `RadioButton` in template property, in which the Toolbar item type set as `Input`.

* Related `RadioButton` component properties are also can be configured like as below.

```javascript
new RadioButton({ label: 'Radio', name: 'default', checked: true })
```

Above steps applicable for all 'Syncfusion' input based components.

{% tab template="toolbar/toolbar-items", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { ToolbarComponent } from '@syncfusion/ej2-angular-navigations';
import { NumericTextBox} from '@syncfusion/ej2-inputs';
import { DropDownList} from '@syncfusion/ej2-dropdowns';
import { CheckBox, RadioButton  } from '@syncfusion/ej2-buttons';

@Component({
    selector: 'app-container',
    template: `
        <ejs-toolbar (created)="onCreate($event)">
          <e-items>
             <e-item text='Cut'></e-item>
             <e-item text='Copy'></e-item>
             <e-item type='Separator'></e-item>
             <e-item text='Undo'></e-item>
             <e-item text='Redo'></e-item>
             <e-item template=' <input id="numeric" type="text" />' type = 'Input'></e-item>
             <e-item template='<input type="text" tabindex="1" id="ddlelement" />' type = 'Input'></e-item>
             <e-item template='<input id="chkelement" type="checkbox"/>' type = 'Input'></e-item>
             <e-item template='<input id="rdelement" type="radio"/>' type = 'Input'></e-item>
          </e-items>
        </ejs-toolbar>
        `
})

export class AppComponent {
    @ViewChild('element') element;
    public data: string[] = ['Badminton', 'Basketball', 'Cricket', 'Golf', 'Hockey', 'Rugby'];
    public templateEle: any = new NumericTextBox({ format: 'c2', value: 1, width: 150 });
    public templateDropdown: any = new DropDownList({ dataSource: this.data, width: 120, index: 2 });
    public templateCheckbox: any = new CheckBox({ label: 'Checkbox', checked: true });
    public templateRadiobutton: any = new RadioButton({ label: 'Radio', name: 'default', checked: true });
    public onCreate (e: any) {
      this.templateCheckbox.appendTo('#chkelement');
      this.templateDropdown.appendTo('#ddlelement');
      this.templateEle.appendTo('#numeric');
      this.templateRadiobutton.appendTo('#rdelement');
    }
}
```

{% endtab %}

## See Also

* [How to set item wise custom template](./how-to/set-item-wise-custom-template/)