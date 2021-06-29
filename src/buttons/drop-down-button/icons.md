---
title: "DropDownButton Icons"
component: "DropDownButton"
description: "Angular DropDownButton allows the end user to place the icons/sprite images in DropDownButton."
---

# Icons

## DropDownButton icons

DropdownButton can have an icon to provide the visual representation of the action. To place the icon on a DropdownButton,
set the [`iconCss`](../api/drop-down-button#iconcss) property to `e-icons` with the required icon CSS. By default,
the icon is positioned to the left side of the DropdownButton. You can customize the icon's position using
the [`iconPosition`](../api/drop-down-button#iconposition) property.

In the following example, the DropdownButton with default iconPosition and iconPosition as `Top` is showcased.

{% tab template="drop-down-button/dd-icons", sourceFiles="app/**/*.ts,styles.css", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { ItemModel } from '@syncfusion/ej2-angular-splitbuttons';

@Component({
    selector: 'app-root',
    template: `<!-- To render DropDownButton. -->
               <button ejs-dropdownbutton [items]='items' content='Message' iconCss='ddb-icons e-message'></button>
               <!-- To render DropDownButton with iconposition as 'top'. -->
               <button ejs-dropdownbutton [items]='items' content='Message' iconCss='ddb-icons e-message' iconPosition='Top'></button>`
})

export class AppComponent {
   // Initialize action items.
   public items: ItemModel[] = [
    {
        text: 'Edit'
    },
    {
        text: 'Delete'
    },
    {
        text: 'Mark as Read'
    },
    {
        text: 'Like Message'
    }];

}
```

{% endtab %}

### Icon only DropDownButton

Icon only DropDownButton can be achieved by using [`iconCss`](../api/drop-down-button#iconcss) property and to hide drop
down arrow `e-caret-hide` class is added using [`cssClass`](../api/drop-down-button#cssclass) property.

{% tab template="drop-down-button/icon-only", sourceFiles="app/**/*.ts,styles.css", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';
import { ItemModel } from '@syncfusion/ej2-angular-splitbuttons';

@Component({
    selector: 'app-root',
    template: `<!-- To render DropDownButton without down arrow. -->
               <button ejs-dropdownbutton [items]='items' iconCss='e-icons e-menu' cssClass='e-caret-hide'></button>`
})

export class AppComponent {
   // Initialize action items.
   public items: ItemModel[] = [
    {
        text: 'New tab'
    },
    {
        text: 'New window'
    },
    {
        text: 'New incognito window'
    },
    {
        separator: true
    },
    {
        text: 'Print'
    },
    {
        text: 'Cast'
    },
    {
        text: 'Find'
    }];

}
```

{% endtab %}

> The Essential JS 2 provides a set of icons that can be loaded by applying `e-icons` class name to the element.
You can also use third party icons on the DropDownButton using the [`iconCss`](../api/drop-down-button#iconcss) property.

### DropDownButton with sprite image

Sprite images can be loaded in DropDownButton instead of font icons using [`iconCss`](../api/drop-down-button#iconcss) property.

In this following example, `e-image` class is added with background url of the sprite image along with X and Y positions. The `width` and
`height` of the element set as `32px`.

{% tab template="drop-down-button/sprite", sourceFiles="app/**/*.ts,styles.css", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';
import { ItemModel } from '@syncfusion/ej2-angular-splitbuttons';

@Component({
    selector: 'app-root',
    template: `<!-- To render DropDownButton with sprite image. -->
               <button ejs-dropdownbutton [items]='items' iconCss='e-image' cssClass='e-caret-hide'></button>`
})

export class AppComponent {
   // Initialize action items.
   public items: ItemModel[] = [
    {
        text: 'Display Settings'
    },
    {
        text: 'System Settings'
    },
    {
        text: 'Additional Settings'
    }];

}
```

{% endtab %}

> The Essential JS 2 provides a set of icons that can be loaded by applying `e-icons` class name to the element.
You can also use third party icons on the DropDownButton using the [`iconCss`](../api/drop-down-button#iconcss) property.

## Vertical button

Vertical button in DropDownButton can be achieved by adding `e-vertical` class
using [`cssClass`](../api/drop-down-button#cssclass) property.

{% tab template="drop-down-button/vertical", sourceFiles="app/**/*.ts,styles.css", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { ItemModel } from '@syncfusion/ej2-angular-splitbuttons';

@Component({
    selector: 'app-root',
    template: `<!-- To render Vertical DropDownButton. -->
               <button ejs-dropdownbutton [items]='items' content='Message' iconCss='ddb-icons e-message' cssClass='e-vertical' iconPosition='Top'></button>`
})

export class AppComponent {
   // Initialize action items.
   public items: ItemModel[] = [
    {
        text: 'Edit'
    },
    {
        text: 'Delete'
    },
    {
        text: 'Mark as Read'
    },
    {
        text: 'Like Message'
    }];

}
```

{% endtab %}

## See Also

* [Dropdown popup with icons](./popup-items#icons)
* [Customized icon size](./how-to/customize-icon-and-width)