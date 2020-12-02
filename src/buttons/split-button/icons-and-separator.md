---
title: "SplitButton Icons and Separator"
component: "SplitButton"
description: "Angular SplitButton allows the end user to place the icons and separate popup items in SplitButton. "
---

# Icons and separator

## SplitButton Icons

SplitButton can have an icon to provide the visual representation of the action. To place the icon on a SplitButton,
set the [`iconCss`](../api/split-button#iconcss) property to `e-icons` with the required icon CSS. By default,
the icon is positioned to the left side of the SplitButton. You can customize the icon's position by using
the [`iconPosition`](../api/split-button#iconposition) property

The following example illustrates how to place icon in SplitButton component.

{% tab template="split-button/icon", sourceFiles="app/**/*.ts,styles.css", isDefaultActive=true %}

 ```typescript
import { Component } from '@angular/core';
import { ItemModel } from '@syncfusion/ej2-angular-splitbuttons';

@Component({
    selector: 'app-root',
    template: `<!-- To Render splitbutton. -->
               <ejs-splitbutton content="Paste" [items]='items' iconCss="e-sb-icons e-paste"></ejs-splitbutton>
               <ejs-splitbutton content="Paste" [items]='items' iconCss="e-sb-icons e-paste" iconPosition="Top"></ejs-splitbutton>`
})

export class AppComponent {
  public items: ItemModel[] = [
    {
        text: 'Cut'
    },
    {
        text: 'Copy'
    },
    {
        text: 'Paste'
    }
     ];
}
```

{% endtab %}

> The Essential JS 2 provides a set of icons that can be loaded by applying `e-icons` class name to the element.
You can also use third party icons on the splitBtn using the `iconCss`property.

### Vertical Button

Vertical Button in SplitButton can be achieved by adding `e-vertical` class using [`cssClass`](../api/split-button#cssclass)
property.

The following example illustrates how to vertical support in SplitButton component.

{% tab template="split-button/vertical", sourceFiles="app/**/*.ts,styles.css", isDefaultActive=true %}

 ```typescript
import { Component } from '@angular/core';
import { ItemModel } from '@syncfusion/ej2-angular-splitbuttons';

@Component({
    selector: 'app-root',
    template: `<!-- To Render splitbutton. -->
               <ejs-splitbutton content="Paste" [items]='items' iconCss="e-sb-icons e-paste" cssClass="e-vertical" iconPosition="Top"></ejs-splitbutton>`
})

export class AppComponent {
  public items: ItemModel[] = [
    {
        text: 'Cut'
    },
    {
        text: 'Copy'
    },
    {
        text: 'Paste'
    }
     ];
}
```

{% endtab %}

> The Essential JS 2 provides a set of icons that can be loaded by applying `e-icons` class name to the element.
You can also use third party icons on the SplitButton using the `iconCss`property.

## Separator

SplitButton component has Separator support. This can be achieved by setting `separator` as `true`.

The following example illustrates how to enable separator support in SplitButton component.

{% tab template="split-button/separator", sourceFiles="app/**/*.ts,styles.css", isDefaultActive=true %}

 ```typescript
import { Component } from '@angular/core';
import { ItemModel } from '@syncfusion/ej2-angular-splitbuttons';

@Component({
    selector: 'app-root',
    template: `<!-- To Render splitbutton. -->
               <ejs-splitbutton content="Paste" [items]='items' iconCss="e-sb-icons e-paste"></ejs-splitbutton>`
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
    },
    {
        separator: true
    },
    {
        text: 'Font',
        iconCss: 'e-sb-icons e-font'
    },
    {
        text: 'Paragraph',
        iconCss: 'e-sb-icons e-paragraph'
    }];
}
```

{% endtab %}

## See Also

* [SplitButton popup with icons](./popup-items#icons)
