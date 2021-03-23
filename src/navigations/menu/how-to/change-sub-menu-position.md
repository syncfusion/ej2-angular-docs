# Change sub menu position

The submenu position can be changed by using the [`beforeOpen`](../../api/menu/#beforeopen) event. Assign the top and left position where you want to open the submenu to the [`beforeOpen`](../../api/menu/#beforeopen) event arguments `args.top` and `args.left` respectively.

In the below sample, the sub menu opens above the parent menu item.

{% tab template="menu/position", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { enableRipple, closest } from '@syncfusion/ej2-base';
import { MenuItemModel, BeforeOpenCloseMenuEventArgs } from '@syncfusion/ej2-angular-navigations';

enableRipple(true);

@Component({
    selector: 'app-root',
    template: `<!-- To Render Menu. -->
            <ejs-menu [items]='menuItems' (beforeOpen)='onBeforeOpen($event)'></ejs-menu>`
})

export class AppComponent {
    menuItems: MenuItemModel[] = [
    {
        text: 'File',
        items: [
            { text: 'Open' },
            { text: 'Save' },
            { text: 'Exit' }
        ]
    },
    {
        text: 'Edit',
        items: [
            { text: 'Cut' },
            { text: 'Copy' },
            { text: 'Paste' }
        ]
    },
    {
        text: 'View',
        items: [
            { text: 'Toolbar' },
            { text: 'Sidebar' }
        ]
    },
    {
        text: 'Tools',
        items: [
            { text: 'Spelling & Grammar' },
            { text: 'Customize' },
            { text: 'Options' }
        ]
    },
    { text: 'Go' },
    { text: 'Help' }];

    onBeforeOpen(args: BeforeOpenCloseMenuEventArgs): void {
        // Getting parent menu item element offset
        let relativeOffset: ClientRect = closest(args.event.target as Element, '.e-menu-item').getBoundingClientRect();
        // Getting sub menu wrapper element using closest method
        let subMenuEle: HTMLElement = closest(args.element, '.e-menu-wrapper') as HTMLElement;
        subMenuEle.style.display = 'block';
        args.top = (relativeOffset.top - subMenuEle.getBoundingClientRect().height) + pageYOffset;
        args.left = relativeOffset.left + pageXOffset;
        subMenuEle.style.display = '';
    }
}
```

{% endtab %}

>> For custom positioning, set both `top` and `left` position in the [`beforeOpen`](../../api/menu/#beforeopen) event.
