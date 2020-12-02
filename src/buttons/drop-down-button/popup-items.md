---
title: "DropDownButton Popup Items"
component: "DropDownButton"
description: "Angular DropDownButton allows the end user to customize the whole popup or action items in popup using templates, navigate to other pages on action item click."
---

# Popup items

## Icons

The popup action item have an icon or image to provide visual representation of the action. To place the icon on a popup item,
set the [`iconCss`](../api/drop-down-button#iconcss) property to `e-icons` with the required icon CSS. By default, the icon is
positioned to the left side of the popup action item.

In the following sample, the icons for edit, delete, mark as read  and like message menu items are
added using the iconCss property.

{% tab template="drop-down-button/popup-icon", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { ItemModel } from '@syncfusion/ej2-angular-splitbuttons';

@Component({
    selector: 'app-root',
    template: `<!-- To render DropDownButton. -->
               <button ejs-dropdownbutton [items]='items' content='Message' iconCss='ddb-icons e-message'></button>`
})

export class AppComponent {
   // Initialize action items.
   public items: ItemModel[] = [
    {
        text: 'Edit',
        iconCss: 'ddb-icons e-edit'
    },
    {
        text: 'Delete',
        iconCss: 'ddb-icons e-delete'
    },
    {
        text: 'Mark As Read',
        iconCss: 'ddb-icons e-read'
    },
    {
        text: 'Like Message',
        iconCss: 'ddb-icons e-like'
    }];

}
```

{% endtab %}

## Navigations

Actions in DropDownButton can be used to navigate to the other web
page when action item is clicked. This can be achieved by
providing link to the action item using `url` property.

In the following sample, navigation URL for Flipkart, Amazon, and
Snapdeal action items are added using the `url` property:

{% tab template="drop-down-button/navigation", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { ItemModel, MenuEventArgs } from '@syncfusion/ej2-angular-splitbuttons';

@Component({
    selector: 'app-root',
    template: `<!-- To render DropDownButton. -->
               <button ejs-dropdownbutton [items]='items' content='Shop By' iconCss='e-cart-icon e-shopping' (beforeItemRender)='itemBeforeEvent($event)'></button>`
})

export class AppComponent {
   // Initialize action items.
   public items: ItemModel[] = [
    {
        text: 'Flipkart',
        iconCss: 'e-cart-icon e-link',
        url: 'https://www.google.co.in/search?q=flipkart'
    },
    {
        text: 'Amazon',
        iconCss: 'e-cart-icon e-link',
        url: 'https://www.google.co.in/search?q=amazon'
    },
    {
        text: 'Snapdeal',
        iconCss: 'e-cart-icon e-link',
        url: 'https://www.google.co.in/search?q=snapdeal'
    }];
    // To open the url in the blank page.
    public itemBeforeEvent (args: MenuEventArgs) {
        args.element.getElementsByTagName('a')[0].setAttribute('target', '_blank');
    }

}
```

{% endtab %}

## Template

### Item templating

Popup items can be customized using the [`beforeItemRender`](../api/drop-down-button#beforeitemrender) event. The item render event
triggers while rendering each popup action item. The event argument will be used to identify the action item and
customize based on the requirement.

The following popup template is customized using `beforeItemRender` event by appending `span` and `div` element on each `li` rendering:

{% tab template="drop-down-button/template", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { ItemModel, MenuEventArgs } from '@syncfusion/ej2-angular-splitbuttons';

@Component({
    selector: 'app-root',
    template: `<!-- To render DropDownButton. -->
               <button ejs-dropdownbutton [items]='items' content='Paste' iconCss='e-ddb-icons e-paste' iconPosition='Top' cssClass='e-vertical' (beforeItemRender)='itemBeforeEvent($event)'></button>`
})

export class AppComponent {
   // Initialize action items.
   public items: ItemModel[] = [
    {
        text: 'Edit'
    },
    {
        text: 'Cut'
    }];

    public itemBeforeEvent (args: MenuEventArgs) {
    // To append span and div element in each li rendering.
    if (args.item.text === 'Edit') {
      args.element.innerHTML = '<span></span><div><b>Paste Text</b><div>Provides option to paste only the<br>selected text.</div></div>';
      args.element.style.height = '80px';
      let span: Element = args.element.children[0];
      span.setAttribute('class','e-cm-icons e-pastetext e-align');
      let div: Element = args.element.children[1];
      div.setAttribute('class', 'e-div-align');
    } else {
      args.element.innerHTML = '<span></span><div><b>Paste Special</b><div>Provides options to paste formulas,<br> values, comments, validations etc...</div></div>';
      args.element.style.height = '80px';
      let span: Element = args.element.children[0];
      span.setAttribute('class','e-cm-icons e-pastespecial e-align');
      let div: Element = args.element.children[1];
      div.setAttribute('class', 'e-div-align');
    }
    }
}
```

{% endtab %}

### Popup templating

The whole popup can be customized as per the requirement. In the following example, the popup can be
customized by handling it in [`target`](../api/drop-down-button#target) property.

In the following sample, the whole popup item is customized as table template by giving `div` as target and it can be achieved
using `target` property.

{% tab template="drop-down-button/popup", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<!-- Target element to DropDownButton . -->
               <div id="target" style='border: 1px solid #999;'>
               <!-- To create table. -->
               <table>
               <caption style='height: 18px; background-color: #e0e0e0;'><b>Insert Table</b></caption>
                    <tr class='e-row'>
                        <td class='e-data'></td>
                        <td class='e-data'></td>
                        <td class='e-data'></td>
                        <td class='e-data'></td>
                        <td class='e-data'></td>
                        <td class='e-data'></td>
                    </tr>
                    <tr class='e-row'>
                        <td class='e-data'></td>
                        <td class='e-data'></td>
                        <td class='e-data'></td>
                        <td class='e-data'></td>
                        <td class='e-data'></td>
                        <td class='e-data'></td>
                    </tr>
                    <tr class='e-row'>
                        <td class='e-data'></td>
                        <td class='e-data'></td>
                        <td class='e-data'></td>
                        <td class='e-data'></td>
                        <td class='e-data'></td>
                        <td class='e-data'></td>
                    </tr>
                    <tr class='e-row'>
                        <td class='e-data'></td>
                        <td class='e-data'></td>
                        <td class='e-data'></td>
                        <td class='e-data'></td>
                        <td class='e-data'></td>
                        <td class='e-data'></td>
                    </tr>
                    <tr class='e-row'>
                        <td class='e-data'></td>
                        <td class='e-data'></td>
                        <td class='e-data'></td>
                        <td class='e-data'></td>
                        <td class='e-data'></td>
                        <td class='e-data'></td>
                    </tr>
                    <tr class='e-row'>
                        <td class='e-data'></td>
                        <td class='e-data'></td>
                        <td class='e-data'></td>
                        <td class='e-data'></td>
                        <td class='e-data'></td>
                        <td class='e-data'></td>
                    </tr>
                </table>
               </div>
               <!-- To render DropDownButton. -->
               <button ejs-dropdownbutton target='#target' content='Table' iconCss='e-icons e-table' iconPosition='Top' cssClass='e-vertical'></button>`
})

export class AppComponent {
}

```

{% endtab %}

## Separator

The Separators are the horizontal lines that are used to separate the popup items. You cannot select the separators.
You can enable separators to group the popup items using the `separator` property.

In the following sample, cut, copy, and paste popup items are grouped using the separator property:

{% tab template="drop-down-button/accessibility", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { ItemModel } from '@syncfusion/ej2-angular-splitbuttons';

@Component({
    selector: 'app-root',
    template: `<!-- To render DropDownButton. -->
               <button ejs-dropdownbutton [items]='items' content='Clipboard' iconCss='e-icons e-edit'></button>`
})

export class AppComponent {
   // Initialize action items.
   public items: ItemModel[] = [
    {
        text: 'Cut',
        iconCss: 'e-db-icons e-cut'
    },
    {
        text: 'Copy',
        iconCss: 'e-icons e-copy'
    },
    {
        text: 'Paste',
        iconCss: 'e-db-icons e-paste'
    },
    {
        separator: true
    },
    {
        text: 'Font',
        iconCss: 'e-db-icons e-font'
    },
    {
        text: 'Paragraph',
        iconCss: 'e-db-icons e-paragraph'
    }];
}
```

{% endtab %}

## See Also

* [Integration with ListView component](./how-to/group-popup-items-with-listview-component)