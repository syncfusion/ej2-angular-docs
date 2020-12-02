---
title: "Getting Started"
component: "Textbox"
description: "Helps to get started with text box component along with its key features such as a floating label, adding icons (input group), and ripple effect."
---

# Getting Started

This section briefly explains about how to create a simple TextBox through CSS classes using Angular seed repository.

## Dependencies

The following list of dependencies are required to use the TextBox component in your application.

```js
|-- @syncfusion/ej2-angular-inputs
    |-- @syncfusion/ej2-angular-base
    |-- @syncfusion/ej2-inputs
        |-- @syncfusion/ej2-base

```

## Setup angular environment

Angular provides the easiest way to set angular CLI projects using [`Angular CLI`](https://github.com/angular/angular-cli) tool.

Install the CLI application globally to your machine.

```bash
npm install -g @angular/cli
```

## Create a new application

```bash
ng new syncfusion-angular-textbox
```

By default, it install the CSS style base application. To setup with SCSS, pass --style=scss argument on create project.

Example code snippet.

```bash
ng new syncfusion-angular-textbox --style=scss
```

Navigate to the created project folder.

```bash
cd syncfusion-angular-textbox
```

## Adding TextBox package

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) registry.

To install TextBox component, use the following command.

```bash
npm install @syncfusion/ej2-angular-inputs --save
(or)
npm i @syncfusion/ej2-angular-inputs --save
```

> The **--save** will instruct NPM to include the TextBox package inside of the [dependencies](./getting-started#dependencies) section of the `package.json`.

## Adding TextBox to the application

* Modify the template as HTML input element with `e-input`class in `app.component.ts` file to render the `TextBox` component.

```javascript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<input class="e-input" type="text" placeholder="Enter Name" />`
})

export class AppComponent { }
```

## Adding CSS reference

The following CSS files are available in `../node_modules/@syncfusion` package folder.
This can be referenced in [src/styles.css] using following code.

```css
@import '../node_modules/@syncfusion/ej2-base/styles/material.css';
@import '../node_modules/@syncfusion/ej2-inputs/styles/material.css';
@import '../node_modules/@syncfusion/ej2-angular-inputs/styles/material.css';
```

> The [Custom Resource Generator (CRG)](https://crg.syncfusion.com/) is an online web tool, which can be used to generate the custom script and styles for a set of specific components.
> This web tool is useful to combine the required component scripts and styles in a single file.

## Adding icons to the TextBox

You can create a TextBox with icon as a group by creating the parent div element with the class `e-input-group` and
add the icon element as span with the class `e-input-group-icon`. For detailed information, refer to the [Groups](./groups/) section.

```javascript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<div class="wrap">
                <div class="e-input-group">
                <input class="e-input" name='input' type="text" (focus)="focusIn($event.target)"
                placeholder = "Enter Date" (blur)="focusOut($event.target)"/>
                <span class="e-input-group-icon e-input-popup-date" (mouseup)="onMouseUp($event.target)" (mousedown)="onMouseDown($event.target)"></span>
                </div>
              </div>`
})

export class AppComponent {
    public focusIn(target: HTMLElement): void {
        target.parentElement.classList.add('e-input-focus');
    }

    public focusOut(target: HTMLElement): void {
        target.parentElement.classList.remove('e-input-focus');
    }

    public onMouseDown(target: HTMLElement): void {
        target.classList.add('e-input-btn-ripple');
    }

    public onMouseUp(target: HTMLElement): void {
        let ele: HTMLElement = target;
        setTimeout(
                () => {ele.classList.remove('e-input-btn-ripple'); },
                500);
    }
}
```

## Running the application

After completing the configuration required to render a basic TextBox, run the following command to display the output in your default browser.

```cmd
ng serve
```

The following example illustrates the output in your browser.

{% tab template="textbox/icon-support", sourceFiles="app/**/*.ts,index.css", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<div class="wrap">
                <div class="e-input-group">
                <input class="e-input" name='input' type="text" (focus)="focusIn($event.target)"
                placeholder = "Enter Date" (blur)="focusOut($event.target)"/>
                <span class="e-input-group-icon e-input-popup-date" (mouseup)="onMouseUp($event.target)" (mousedown)="onMouseDown($event.target)"></span>
                </div>
              </div>`
})

export class AppComponent {
    public focusIn(target: HTMLElement): void {
        target.parentElement.classList.add('e-input-focus');
    }

    public focusOut(target: HTMLElement): void {
        target.parentElement.classList.remove('e-input-focus');
    }

    public onMouseDown(target: HTMLElement): void {
        target.classList.add('e-input-btn-ripple');
    }

    public onMouseUp(target: HTMLElement): void {
        let ele: HTMLElement = target;
        setTimeout(
                () => {ele.classList.remove('e-input-btn-ripple'); },
                500);
    }
}
```

{% endtab %}

## Floating label

The floating label TextBox floats the label above the TextBox after focusing, or filled with value in the TextBox.
You can create the floating label TextBox by using the [floatLabelType](../api/textbox/#floatlabeltype) API.

{% tab template="textbox/textbox-component", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<div class="wrap">
    <h4>Floating label as auto</h4>
    <div class='textboxes'>
      <ejs-textbox placeholder="First Name" floatLabelType="Auto"></ejs-textbox>
    </div>

    <h4>Floating label as always</h4>
    <div class='textboxes'>
      <ejs-textbox placeholder="First Name" floatLabelType="Always"></ejs-textbox>
    </div>
  </div>`
})

export class AppComponent { }
```

{% endtab %}

## See Also

* [How to render TextBox programmatically](./how-to/add-textbox-programmatically)
* [How to add floating label to TextBox programmatically](./how-to/add-floating-label-to-textbox-programmatically)
