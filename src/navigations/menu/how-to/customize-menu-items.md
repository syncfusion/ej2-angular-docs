# Customize menu items

## Add or remove menu items

Menu items can be added or removed using the [`insertAfter`](../api/menu#insertafter),
[`insertBefore`](../api/menu#insertbefore) and [`removeItems`](../api/menu#removeitems) methods.

In the following example, the **Europe** menu items are added before the **Oceania** item,
the **Africa** menu items are added after the **Asia**, and the **South America**
and **Mexico** items are removed from menu.

{% tab template="menu/getting-started", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { enableRipple } from '@syncfusion/ej2-base';
import { MenuComponent, FieldSettingsModel } from '@syncfusion/ej2-angular-navigations';

enableRipple(true);

@Component({
    selector: 'app-root',
    template: `<!-- To Render Menu. -->
            <ejs-menu #menu [items]='data' [fields]='menuFields' (created)='created()'></ejs-menu>`
})

export class AppComponent {
    @ViewChild('menu')
    private menuObj: MenuComponent;

    //Menu datasource
    private data: { [key: string]: Object }[] = [
        {
            continent: 'Asia',
            countries: [
                { country: 'China' },
                { country: 'India' },
                { country: 'Japan' }
            ]
        },
        {
            continent: 'North America',
            countries: [
                { country: 'Canada' },
                { country: 'Mexico' },
                { country: 'USA' }
            ]
        },
        {
            continent: 'South America',
            countries: [
                { country: 'Brazil' },
                { country: 'Colombia' },
                { country: 'Argentina' }
            ]
        },
        {
            continent: 'Oceania',
            countries: [
                { country: 'Australia' },
                { country: 'New Zealand' },
                { country: 'Samoa' },
            ]
        },
        { continent: 'Antarctica' }
    ];

    //Menu fields definition
    private menuFields: FieldSettingsModel = {
        text: ['continent', 'country'],
        children: ['countries']
    };

    private created(): void {
        let insertItem: { [key: string]: Object }[] = [
            {
                continent: 'Europe',
                countries: [
                    { country: 'Finland' },
                    { country: 'Austria' }
                ]
            }
        ];
        //Add items before to 'Oceania'
        this.menuObj.insertBefore(insertItem, 'Oceania', false);

        insertItem = [
            {
                continent: 'Africa',
                countries: [
                    { country: 'Nigeria' }
                ]
            }
        ];

        //Add items after to 'Asia'
        this.menuObj.insertAfter(insertItem, 'Asia', false);

        //Remove items
        this.menuObj.removeItems(['South America', 'Mexico'], false);
    }
}
```

{% endtab %}

> To process items with `ID` values, set `isUnique` to `true`.

## Enable or disable menu items

You can enable and disable the menu items using the [`enableItems`](../api/menu#enableitems)
method in Menu. To enable menuItems, set the `enable` property in argument to `true` and vice-versa.

In the following example, the **Directory** header item, **Conferences**, and **Music** sub menu items are disabled.

{% tab template="menu/enable-disable", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { enableRipple } from '@syncfusion/ej2-base';
import { MenuComponent, MenuItemModel, BeforeOpenCloseMenuEventArgs } from '@syncfusion/ej2-angular-navigations';

enableRipple(true);

@Component({
    selector: 'app-root',
    template: `<div class="control-section">
            <button ejs-button (click)='btnClick()'>Enable all items</button>
            <div class="menu-section">
                <ejs-menu #menu [items]='menuItems' (beforeOpen)='beforeOpen($event)' (created)='created()'></ejs-menu>
            </div>
        </div>`
})

export class AppComponent {
    @ViewChild('menu')
    private menuObj: MenuComponent;

    //Menu items definition
    private menuItems: MenuItemModel[] = [
        {
            text: 'Events',
            items: [
                { text: 'Conferences' },
                { text: 'Music' },
                { text: 'Workshops' }
            ]
        },
        {
            text: 'Movies',
            items: [
                { text: 'Now Showing' },
                { text: 'Coming Soon' }
            ]
        },
        {
            text: 'Directory',
            items: [
                { text: 'Media Gallery' },
                { text: 'Newsletters' }
            ]
        },
        {
            text: 'Queries',
            items: [
                { text: 'Our Policy' },
                { text: 'Site Map' }
            ]
        },
        { text: 'Services' }
    ];

    private disableItems: string[] = ['Conferences', 'Music', 'Directory'];

    private beforeOpen(args: BeforeOpenCloseMenuEventArgs): void {
        //Handling sub menu items
        for (let i: number = 0; i < args.items.length; i++) {
            if (this.disableItems.indexOf(args.items[i].text) > -1) {
                this.menuObj.enableItems([args.items[i].text], false, false);
            }
        }
    }

    private created(): void {
        //Disable items
        this.menuObj.enableItems(this.disableItems, false, false);
    }

    private btnClick(): void {
        //Enable items
        this.menuObj.enableItems(this.disableItems, true, false);
        this.disableItems = [];
    }
}
```

{% endtab %}

> To disable sub menu items, use the [`beforeOpen`](../api/menu#beforeopen) event.

## Hide or show menu items

You can show or hide the menu items using the [`showItems`](../api/menu#showitems)
and [`hideItems`](../api/menu#hideitems) methods.

In the following example, the **Movies** header item, **Workshops**, and **Music** sub menu items
are hidden in menu.

{% tab template="menu/enable-disable", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { enableRipple } from '@syncfusion/ej2-base';
import { MenuComponent, MenuItemModel, BeforeOpenCloseMenuEventArgs } from '@syncfusion/ej2-angular-navigations';

enableRipple(true);

@Component({
    selector: 'app-root',
    template: `<div class="control-section">
            <button ejs-button (click)='btnClick()'>Show all items</button>
            <div class="menu-section">
                <ejs-menu #menu [items]='menuItems' (beforeOpen)='beforeOpen($event)' (created)='created()'></ejs-menu>
            </div>
        </div>`
})

export class AppComponent {
    @ViewChild('menu')
    private menuObj: MenuComponent;
    private menuItems: MenuItemModel[] = [
        {
            text: 'Events',
            items: [
                { text: 'Conferences' },
                { text: 'Music' },
                { text: 'Workshops' }
            ]
        },
        {
            text: 'Movies',
            items: [
                { text: 'Now Showing' },
                { text: 'Coming Soon' }
            ]
        },
        {
            text: 'Directory',
            items: [
                { text: 'Media Gallery' },
                { text: 'Newsletters' }
            ]
        },
        {
            text: 'Queries',
            items: [
                { text: 'Our Policy' },
                { text: 'Site Map' }
            ]
        },
        { text: 'Services' }
    ];

    private hiddenItems: string[] = ['Workshops', 'Music', 'Movies'];

    private beforeOpen(args: BeforeOpenCloseMenuEventArgs): void {
        //Handling sub menu items
        for (let i: number = 0; i < args.items.length; i++) {
            if (this.hiddenItems.indexOf(args.items[i].text) > -1) {
                this.menuObj.hideItems([args.items[i].text], false);
            }
        }
    }

    private created(): void {
        // Disable menu items
        this.menuObj.hideItems(this.hiddenItems, false);
    }

    private btnClick(): void {
        // Show menu items
        this.menuObj.showItems(this.hiddenItems, false);
        this.hiddenItems = [];
    }
}
```

{% endtab %}

> Using the [`beforeOpen`](../api/menu#beforeopen) event, you can hide the sub menu items as in the above example since the menu supports to hide items only for headers initially.
