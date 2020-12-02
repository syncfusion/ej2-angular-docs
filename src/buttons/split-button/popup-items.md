---
title: "SplitButton Popup Items"
component: "SplitButton"
description: "Angular SplitButton allows the end user to customize the whole popup or action items in popup using templates, and to place icons in popup items."
---

# Popup Items

## Icons

The Popup action item have an icon or image to provide visual representation of the action. To place the icon on a popup item,
set the [`iconCss`](../api/split-button#iconcss) property to `e-icons` with the required icon CSS. By default,
the icon is positioned to the left side of the popup action item.

In the following sample, the icons for Cut, Copy and Paste menu items are
added using the iconCss property.

{% tab template="split-button/popup-icon", sourceFiles="app/**/*.ts,styles.css", isDefaultActive=true %}

 ```typescript
import { Component } from '@angular/core';
import { ItemModel } from '@syncfusion/ej2-angular-splitbuttons';

@Component({
    selector: 'app-root',
    template: `<!-- To Render splitbutton. -->
               <ejs-splitbutton content="Paste" iconCss ="e-sb-icons e-paste"[items]='items'></ejs-splitbutton>`
})

export class AppComponent {
  public items: ItemModel[] = [
    {
        text: 'Cut',
        iconCss: 'e-sb-icons e-cut'
    },
    {
        text: 'Copy',
        iconCss: 'e-icons e-copy'
    },
    {
        text: 'Paste',
        iconCss: 'e-sb-icons e-paste'
    }
     ];
}

```

{% endtab %}

## Template

### Item Templating

Popup items can be customized by using the [`beforeItemRender`](../api/split-button#beforeitemrender) event.
The item render event triggers while rendering each Popup action item. The event argument will be used to identify the
action item and customize it based on the requirement.

{% tab template="split-button/template", sourceFiles="app/**/*.ts,styles.css", isDefaultActive=true %}

 ```typescript
import { Component } from '@angular/core';
import { ItemModel, MenuEventArgs } from '@syncfusion/ej2-angular-splitbuttons';
import { enableRipple, createElement } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    template: `<!-- To Render splitbutton. -->
               <ejs-splitbutton iconCss ="e-sb-icons e-paste" [items]='items' (beforeItemRender)='addClass($event)'></ejs-splitbutton>`
})

export class AppComponent {
  public items: ItemModel[] = [
    {
       text: 'Cut',
     },
     {
       text: 'Copy',
     },
     {
       text: 'Paste',
      }
     ];

      public addClass(args: MenuEventArgs) {
        let shortCutSpan: HTMLElement = createElement('span');
        let text: string = args.item.text;
        args.element.appendChild(shortCutSpan);
        shortCutSpan.setAttribute('class','shortcut');
        let clsName: string = (text == 'Copy') ? 'e-icons' : 'e-sb-icons';
        shortCutSpan.classList.add(clsName);
        (text === 'Cut') ? shortCutSpan.classList.add('e-cut') : (text === 'Paste') ? shortCutSpan.classList.add('e-paste') : shortCutSpan.classList.add('e-copy');
      }
}

```

{% endtab %}

### Popup Templating

The whole popup can be customized as per the requirement. In the following example, the popup can be
customized by handling it in [`target`](../api/split-button#target) property.

{% tab template="split-button/popup-template", sourceFiles="app/**/*.ts,styles.css", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<!-- To Render splitbutton. -->
    <div id='dropdowntarget'>
          <div id= "first">
              <div id='black'></div>
              <div id='red'></div>
              <div id='green'></div>
              <div id='gray'></div>
              <div id='blue'></div>
              <div id='violet'></div>
              <div id='brown'></div>
              <div id='darkgoldenrod'></div>
              <div id='aquamarine'></div>
        </div>
    </div>
<ejs-splitbutton iconCss ="e-sb-icons e-color" target="#dropdowntarget"></ejs-splitbutton>`
})

export class AppComponent {
}

```

{% endtab %}

## See Also

* [Popup items grouping](./how-to/group-items-in-popup)
* [SplitButton popup with separator](./icons-and-separator#separator)