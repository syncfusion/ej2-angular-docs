---
title: "Multiline"
component: "Textbox"
description: "Explains about multiple lines of text like address, description and feedback are allows to fill in multiline textbox and it can be editable or can copy the text."
---

# Multiline TextBox

This feature allows the textbox to accept one or more lines of text like address, description, comments, and more.

## Create multiline textbox

You can convert the default textbox into the multiline textbox by setting the [multiline](../api/textbox/#multiline) API value as true or pass HTML5 textarea as element to the textbox.

> The multiline textbox allows you to resize it in vertical direction alone.

{% tab template="textbox/textarea", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'app-container',
    styleUrls: ['index.css'],
    template: `<div class="multiline">
                <ejs-textbox [multiline]='true' value= 'Mr. Dodsworth Dodsworth, System Analyst, Studio 103, The Business Center' ></ejs-textbox>
               </div>
              `
})
export class AppComponent {
    constructor() {
    }
}

```

{% endtab %}

## Implementing floating label

You can achieve the floating label behavior in the multiline textbox by setting [floatLabelType](../api/textbox/#floatlabeltype) as 'Auto'. The placeholder text act as floating label to the multiline textbox. You can provide the placeholder text to the multiline textbox either by using the [placeholder](../api/textbox/#placeholder) property or placeholder attribute.

{% tab template="textbox/float", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'app-container',
    styleUrls: ['index.css'],
    template: `<label class="label">float label type auto</label>
                <div class="multiline">
                <ejs-textbox [multiline]='true' floatLabelType='Auto' placeholder='Enter your address' ></ejs-textbox>
               </div>
               <label class="label">float label type always</label>
               <div class="multiline">
                <ejs-textbox [multiline]='true' floatLabelType='Always' placeholder='Enter your address' ></ejs-textbox>
               </div>
               <label class="label">float label type never</label>
               <div class="multiline">
                <ejs-textbox [multiline]='true' floatLabelType='Never' placeholder='Enter your address' ></ejs-textbox>
               </div>
              `
})
export class AppComponent {
    constructor() {
    }
}

```

{% endtab %}

## Auto resizing

By default, you can manually resize the multiline textbox. But you can also create an `auto resizing` multiline textbox with both the initial and dynamic value change. It can be done by calculating the height of the textarea in the created event for initial value update and in the input event for dynamic value update of the auto resize multiline textbox, as explained in the following code sample.

{% tab template="textbox/resize", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'app-container',
    styleUrls: ['index.css'],
    template: `<div class="multiline">
                <ejs-textbox #default [multiline]='true' value= 'Mr. Dodsworth Dodsworth, System Analyst, Studio 103, The Business Center' floatLabelType='Auto' placeholder='Enter your address' (created)="createHandler($event)" (input)='inputHandler($event)' ></ejs-textbox>
               </div>
              `
})
export class AppComponent {
    @ViewChild('default')
    public textareaObj: TextBoxComponent;
    public createHandler(): void {
        this.textareaObj.addAttributes({rows: 1});
        this.textareaObj.element.style.height = "auto";
        this.textareaObj.element.style.height = (this.textareaObj.element.scrollHeight)+"px";
    },
    public inputHandler(): void {
    this.textareaObj.element.style.height = "auto";
    this.textareaObj.element.style.height = (this.textareaObj.element.scrollHeight)+"px";
}
  }

```

{% endtab %}

## Disable resizing

By default, the multiline textbox is rendered with resizable. You can disable the resize of the multiline textbox by applying the following CSS styles.

```CSS
    textarea.e-input,
    .e-float-input textarea,
    .e-float-input.e-control-wrapper textarea,
    .e-input-group textarea,
    .e-input-group.e-control-wrapper textarea {
        resize: none;
    }
```

{% tab template="textbox/disable", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'app-container',
    styleUrls: ['index.css'],
    template: `<div class="multiline">
                <ejs-textbox id='default' [multiline]='true' floatLabelType='Auto' placeholder='Enter your address' ></ejs-textbox>
               </div>
              `
})
export class AppComponent {
    constructor() {
    }
}

```

{% endtab %}

## Limit the text length

By default, the text length of the multiline textbox is unlimited. You can limit the text length by setting the `maxLength` attribute using the [addAttributes](../api/textbox/#addattributes) method.

{% tab template="textbox/maxlength", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'app-container',
    styleUrls: ['index.css'],
    template: `<label class="label">Add maxlength attribute through inline</label>
                <div class="multiline">
                <ejs-textbox [multiline]='true' maxlength='15' floatLabelType='Auto' placeholder='Enter your address' ></ejs-textbox>
               </div>
               <label class="label">Add maxlength attribute through addAttributes method</label>
                <div class="multiline">
                <ejs-textbox #default [multiline]='true' floatLabelType='Auto' placeholder='Enter your address' ></ejs-textbox>
               </div>
               <button ejs-button id=length (click)='clickHandler($event)'>Add max length</button>
               `
})
export class AppComponent {
    @ViewChild('default')
    public textareaObj: TextBoxComponent;

    public clickHandler() {
        this.textareaObj.addAttributes({maxlength: 15});
 }
}

```

{% endtab %}

## Count characters

You can show the number of characters entered inside the textarea by calculating the character count in the input event of multiline textbox. The character count is updated while entering or deleting any character inside the textarea. The character count shows how many characters can be entered or left to be entered.

{% tab template="textbox/count", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'app-container',
    styleUrls: ['index.css'],
    template: `<div class="multiline">
                <ejs-textbox #default [multiline]='true' maxlength='25' floatLabelType='Auto' placeholder='Enter your address' (input)='inputHandler($event)' ></ejs-textbox>
               <span id='numbercount'></span>
               </div>
              `
})
export class AppComponent {
     @ViewChild('default')
    public textareaObj: TextBoxComponent;

    public inputHandler(): void {
    let word, addresscountRem, addressCount;
    word = this.textareaObj.element.value;
    addressCount = word.length;
    addresscountRem = document.getElementById('numbercount');
    addresscountRem.textContent = addressCount+"/25";
    }
}

```

{% endtab %}