# Change animation settings

To change the animation of the Menu, [`animationSettings`](https://ej2.syncfusion.com/angular/documentation/api/menu/menuAnimationSettingsModel/) property is used. The supported effects for Menu are,

| Effect | Functionality |
| ------------ | ----------------------- |
| None | Specifies the sub menu transform with no animation effect. |
| SlideDown | Specifies the sub menu transform with slide down effect. |
| ZoomIn | Specifies the sub menu transform with zoom in effect. |
| FadeIn | Specifies the sub menu transform with fade in effect. |

The following sample illustrates how to open Menu with `FadeIn` [`effect`](https://ej2.syncfusion.com/angular/documentation/api/menu/menuAnimationSettingsModel/#effect) with the [`duration`](https://ej2.syncfusion.com/angular/documentation/api/menu/menuAnimationSettingsModel/#duration) of `800ms`. Also we can set [`easing`](https://ej2.syncfusion.com/angular/documentation/api/menu/menuAnimationSettingsModel/#easing) for menu items.

{% tab template="menu/getting-started", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { enableRipple } from '@syncfusion/ej2-base';
import { MenuItemModel, MenuAnimationSettingsModel } from '@syncfusion/ej2-angular-navigations';

enableRipple(true);

@Component({
    selector: 'app-root',
    template: `<!-- To Render Menu. -->
            <ejs-menu [items]='menuItems' [animationSettings]='animationSettings'></ejs-menu>`
})

export class AppComponent {

    public animationSettings: MenuAnimationSettingsModel = {
        effect: 'FadeIn',
        duration: 800
    }

    public menuItems: MenuItemModel[] = [
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
        { text: 'Help' }
    ];
}
```

{% endtab %}