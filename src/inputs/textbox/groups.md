---
title: "Groups"
component: "Textbox"
description: "Explains how to add icons and clear button to the floating text box that is  achieved with or without the required attribute."
---

# Groups

The following section explains you the steps required to create TextBox with `icon` and `floating label`.

TextBox:

* Create a parent div element with the class `e-input-group`

* Place input element with the class `e-input` inside the parent div element.

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<div class="wrap">
                <div class="e-float-input e-input-group">
                <input class="e-input" type="text" placeholder="Enter Name" />
                </div>
               </div>`
})

export class AppComponent { }
```

Floating label:

* Add the `e-float-input` class to the parent div element.

* Remove the e-input class and add `required` attribute to the input element.

* Place the span element with class `e-float-line` after the input element.

* Place the label element with class `e-float-text` after the above created span element.
When you focus or filled with value in the TextBox, the label floats above the TextBox.

> Creating the Floating label TextBox, you have to set the `required` attribute to the Input element to
achieve the floating label functionality which is used for validating the value existence in TextBox.
If you want to render the Floating label TextBox without
`required` attribute then refer to the [Floating Label without required attribute](#floating-Label-without-required-attribute) section.

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<div class="wrap">
                  <div class="e-float-input e-input-group">
                    <input type="text" required/>
                    <span class="e-float-line"></span>
                    <label class="e-float-text">Enter Name </label>
                  </div>
               </div>`
})

export class AppComponent { }
```

And refer to the following sections to add the icons to the TextBox.

## With icon and floating label

Create an icon element as a span with the class `e-input-group-icon`, and the user can place the icon in either side of TextBox
by adding the created icon element before/after the input.

For the floating label enabled TextBox add the icon element as first or last element inside the TextBox wrapper, and
based on the element position it will act as prefix or suffix icon.

{% tab template="textbox/getting-started", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<div class="wrap">

                <h4> TextBox with icons </h4>

                <div class="e-input-group">
                    <input class="e-input" type="text" (focus)="focusIn($event.target)"
                    placeholder = "Enter Date" (blur)="focusOut($event.target)"/>
                    <span class="e-input-group-icon e-input-popup-date" (mouseup)="onMouseUp($event.target)" (mousedown)="onMouseDown($event.target)"></span>
                </div>

                <div class="e-input-group e-float-icon-left">
                    <span class="e-input-group-icon e-input-date" (mouseup)="onMouseUp($event.target)" (mousedown)="onMouseDown($event.target)"></span>
                    <div class="e-input-in-wrap">
                        <input class="e-input" type="text" (focus)="focusIn($event.target)"
                        placeholder = "Enter Date" (blur)="focusOut($event.target)"/>
                    </div>
                </div>

                <div class="e-input-group e-float-icon-left">
                    <span class="e-input-group-icon e-input-date" (mouseup)="onMouseUp($event.target)" (mousedown)="onMouseDown($event.target)"></span>
                    <div class="e-input-in-wrap">
                        <input class="e-input" type="text" (focus)="focusIn($event.target)"
                        placeholder = "Enter Date" (blur)="focusOut($event.target)"/>
                        <span class="e-input-group-icon e-input-down" (mouseup)="onMouseUp($event.target)" (mousedown)="onMouseDown($event.target)"></span>
                    </div>
                </div>

                <h4> Floating label with icons </h4>

                <div class="e-float-input e-input-group">
                    <input type="text" required (focus)="focusIn($event.target)" (blur)="focusOut($event.target)">
                    <span class="e-float-line"></span>
                    <label class="e-float-text" >Enter Date</label>
                    <span class="e-input-group-icon e-input-popup-date" (mouseup)="onMouseUp($event.target)" (mousedown)="onMouseDown($event.target)"></span>
                </div>

                <div class="e-float-input e-input-group e-float-icon-left">
                    <span class="e-input-group-icon e-input-date" (mouseup)="onMouseUp($event.target)" (mousedown)="onMouseDown($event.target)"></span>
                    <div class="e-input-in-wrap">
                        <input type="text" required (focus)="focusIn($event.target)" (blur)="focusOut($event.target)">
                        <span class="e-float-line"></span>
                        <label class="e-float-text" >Enter Date</label>
                    </div>
                </div>

                <div class="e-float-input e-input-group e-float-icon-left">
                    <span class="e-input-group-icon e-input-date" (mouseup)="onMouseUp($event.target)" (mousedown)="onMouseDown($event.target)"></span>
                    <div class="e-input-in-wrap">
                        <input type="text" required (focus)="focusIn($event.target)" (blur)="focusOut($event.target)">
                        <span class="e-float-line"></span>
                        <label class="e-float-text" >Enter Date</label>
                        <span class="e-input-group-icon e-input-down" (mouseup)="onMouseUp($event.target)" (mousedown)="onMouseDown($event.target)"></span>
                    </div>
                </div>
              </div>`
})

export class AppComponent {
    public focusIn(target: HTMLElement): void {
        let parent: HTMLElement = target.parentElement;
        if (parent.classList.contains('e-input-in-wrap') {
            parent.parentElement.classList.add('e-input-focus');
        } else {
            parent.classList.add('e-input-focus');
        }
    }

    public focusOut(target: HTMLElement): void {
        let parent: HTMLElement = target.parentElement;
        if (parent.classList.contains('e-input-in-wrap') {
            parent.parentElement.classList.remove('e-input-focus');
        } else {
            parent.classList.remove('e-input-focus');
        }
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

> To place the icon on left side of the TextBox, create a div element with the class `e-input-in-wrap` as wrapper to the input
element and place the `floating line`, `floating text`, and right side icon element within it.
Add the `e-float-icon-left` class to the TextBox container element.

## With clear button and floating label

The clear button is added to the input for clearing the value given in the TextBox.
It is shown only when the input field has a value, otherwise not shown.

You can add the clear button to the TextBox by `showClearButton` API in textbox

{% tab template="textbox/textbox-component-clearicons", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<div class="wrap">
    <h4>Textbox with clear icon</h4>
    <div class='textboxes'>
        <ejs-textbox placeholder="First Name" showClearButton='true' floatLabelType="Never"></ejs-textbox>
    </div>

    <h4>Floating Textbox with clear icon</h4>
    <div class='textboxes'>
        <ejs-textbox placeholder="Last Name" showClearButton='true' floatLabelType="Auto"></ejs-textbox>
    </div>
    </div>`
})

export class AppComponent { }
```

{% endtab %}

## Floating Label without required attribute

You can render the `Floating label TextBox` without `required` attribute by manually
float the label above of the TextBox using `ngClass`.
You can manually float the label above of the TextBox by adding the below list of
classes to the floating label element. The classes are:

Class Name        | Description
------------------| -------------
  e-label-top     | Floats the label above of the TextBox.
  e-label-bottom  | Label to be placed as placeholder for the TextBox.

{% tab template="textbox/getting-started", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<div class="wrap">
                <h4> Floating Label without required attribute </h4>
                  <div class="e-float-input e-input-group" [ngClass]="{'e-input-focus': tb1Focused}">
                      <input type="text" id="textBox1" [(ngModel)]="textboxValue"
                      #testTextBox1 (focus)="tb1Focused = true" (blur)="tb1Focused = false"/>
                      <span class="e-float-line"></span>
                      <label class="e-float-text" [ngClass]="{'e-label-top': textboxValue !== '' , 'e-label-bottom':  textboxValue == ''}" >Enter Name</label>
                  </div>
              </div>`
})

export class AppComponent {

    public textboxValue;

     ngOnInit() {
    this.textboxValue = '';
  }
}

```

{% endtab %}

## Multi-line Input with Floating Label

Add the HTML textarea element with the `e-input` class to create default multi-line input.

Add the floating label support to the `multi-line input` by creating the floating label structure as defined in the initial section.

{% tab template="textbox/getting-started", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<div class="wrap">

                <textarea class="e-input" placeholder="Address"></textarea>

                <div class="e-float-input">
                    <textarea required></textarea>
                    <span class="e-float-line"></span>
                    <label class="e-float-text"> Address </label>
                </div>
               </div>`
})

export class AppComponent { }
```

{% endtab %}

## See Also

* [How to add floating label to TextBox programmatically](./how-to/add-floating-label-to-textbox-programmatically)
* [Change the floating label color of the TextBox](./how-to/change-the-floating-label-color-of-the-textbox)
* [Change the color of the TextBox based on its value](./how-to/change-the-color-of-the-textbox-based-on-its-value)
