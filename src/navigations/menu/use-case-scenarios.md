---
title: "Menu use case scenarios"
component: "Menu"
description: "TypeScript Menu how to section, toolbar menu, mobile menu, custom menu, scrollable menu."
---

# Use case scenarios

## Scrollable menu

The menu component supports horizontal and vertical scrolling to render large menus and submenus in an adaptive way. This can be achieved by enabling the [`enableScrolling`](../api/menu/#enablescrolling) property and by restricting the corresponding menu/submenu size.

{% tab template="menu/scroll", sourceFiles="app/**/*.ts,index.css", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { enableRipple, closest } from '@syncfusion/ej2-base';
import { MenuItemModel, BeforeOpenCloseMenuEventArgs } from '@syncfusion/ej2-angular-navigations';

enableRipple(true);

@Component({
    selector: 'app-root',
    template: `<ejs-menu [items]='menuItems' cssClass='e-scrollable-menu' [enableScrolling]="true"  (beforeOpen)='onBeforeOpen($event)'></ejs-menu>`
})

export class AppComponent {
    menuItems: MenuItemModel[] = [
        {
            text: 'Appliances',
            items: [
                {
                    text: 'Kitchen',
                    items: [
                        { text: 'Electric Cookers' },
                        { text: 'Coffee Makers' },
                        { text: 'Blenders' },
                        { text: 'Microwave Ovens' }
                    ]
                },
                {
                    text: 'Television',
                    items: [
                        { text: 'Our Exclusive TVs' },
                        { text: 'Smart TVs' },
                        { text: 'Big Screen TVs' }
                    ]
                },
                {
                    text: 'Washing Machine'
                },
                {
                    text: 'Refrigerators'
                },
                {
                    text: 'Air Conditioners',
                    items: [
                        { text: 'Inverter ACs' },
                        { text: 'Split ACs' },
                        { text: 'Window ACs' },
                    ]
                },
                {
                    text: 'Water Purifiers'
                },
                {
                    text: 'Air Purifiers'
                },
                {
                    text: 'Chimneys'
                },
                {
                    text: 'Inverters'
                },
                {
                    text: 'Healthy Living'
                },
                {
                    text: 'Vacuum Cleaners'
                },
                {
                    text: 'Room Heaters'
                },
                {
                    text: 'New Launches'
                }
            ]
        },
        {
            text: 'Accessories',
            items: [
                {
                    text: 'Mobile',
                    items: [
                        { text: 'Headphones' },
                        { text: 'Memory Cards' },
                        { text: 'Power Banks' },
                        { text: 'Mobile Cases' },
                        { text: 'Screen Protectors' }
                    ]
                },
                {
                    text: 'Laptops'
                },
                {
                    text: 'Desktop PC',
                    items: [
                        { text: 'Pendrives' },
                        { text: 'External Hard Disks' },
                        { text: 'Monitors' },
                        { text: 'Keyboards' }
                    ]
                },
                {
                    text: 'Camera',
                    items: [
                        { text: 'Lens' },
                        { text: 'Tripods' }
                    ]
                }
            ]
        },
        {
            text: 'Fashion',
            items: [
                {
                    text: 'Men'
                },
                {
                    text: 'Women'
                }
            ]
        },
        {
            text: 'Home & Living',
            items: [
                {
                    text: 'Furniture'
                },
                {
                    text: 'Decor'
                },
                {
                    text: 'Smart Home Automation'
                },
                {
                    text: 'Dining & Serving'
                }
            ]
        },
        {
            text: 'Entertainment',
            items: [
                {
                    text: 'Televisions'
                },
                {
                    text: 'Home Theatres'
                },
                {
                    text: 'Gaming Laptops'
                }
            ]
        },
        {
            text: 'Contact Us'
        },
        {
            text: 'Help'
        }
    ];

    onBeforeOpen(args: BeforeOpenCloseMenuEventArgs): void {
        // Restricting sub menu wrapper height
        if (args.parentItem.text === 'Appliances') {
            (closest(args.element, '.e-menu-wrapper') as HTMLElement).style.height = '230px';
        }
    }
}
```

{% endtab %}

## Menu in toolbar

The following example demonstrates how to integrate Menu with Toolbar component.

{% tab template="menu/toolbar-menu", sourceFiles="app/**/*.ts,toolbar.css", isDefaultActive=true %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { enableRipple } from '@syncfusion/ej2-base';
import { ToolbarComponent, MenuAnimationSettingsModel } from '@syncfusion/ej2-angular-navigations';

enableRipple(true);

@Component({
    selector: 'app-root',
    template: `<div class="control-section">
                 <div class="toolbar-menu-control">
                    <div id='menu'><ejs-menu [items]='menuItems' [fields]='menuFields' [animationSettings]='animationSettings'></ejs-menu></div>
                 <ejs-toolbar id="shoppingtoolbar" #toolbar (created)='created()'>
                    <e-items>
                        <e-item template='#menu'></e-item>
                        <e-item prefixIcon='em-icons e-shopping-cart' align='Right'></e-item>
                    </e-items>
                 </ejs-toolbar>
                </div>
               </div>
    `
})

export class AppComponent {
    @ViewChild('toolbar')
    private toolbarObj: ToolbarComponent;

    private menuItems: { [key: string]: Object }[] = [
        {
            header: 'Events',
            subItems: [
                { text: 'Conferences' },
                { text: 'Music' },
                { text: 'Workshops' }
            ]
        },
        {
            header: 'Movies',
            subItems: [
                { text: 'Now Showing' },
                { text: 'Coming Soon' }
            ]
        },
        {
            header: 'Directory',
            subItems: [
                { text: 'Media Gallery' },
                { text: 'Newsletters' }
            ]
        },
        {
            header: 'Queries',
            subItems: [
                { text: 'Our Policy' },
                { text: 'Site Map' },
                { text: '24x7 Support' }
            ]
        },
        { header: 'Services' }
    ];

    private menuFields: Object = {
        text: ['header', 'text', 'value'],
        children: ['subItems', 'options']
    };

    private animationSettings: MenuAnimationSettingsModel = { effect: 'None' };

    private created(): void {
        this.toolbarObj.refreshOverflow();
    }
}
```

{% endtab %}

## Hamburger menu

The following example demonstrates the use case of menu with Accordion component integrated in SideBar.

{% tab template="menu/sidebar-menu", sourceFiles="app/**/*.ts,sidebar.css", isDefaultActive=true %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { enableRipple } from '@syncfusion/ej2-base';
import { Accordion } from '@syncfusion/ej2-navigations';
import { SidebarComponent, AccordionComponent, ExpandEventArgs, AccordionClickArgs } from '@syncfusion/ej2-angular-navigations';

enableRipple(true);

@Component({
    selector: 'app-root',
    template: `<div class="header">
        <span id="hamburger" class="e-icons menu default" (click)='hamburgerClick()'></span>
            <div class="content">Header content</div>
        </div>
        <ejs-sidebar #sidebar id='default-sidebar' width='220px' type='Over'>
            <div class="title-header">
                <div style="display:inline-block"> Menu </div>
                <span  id="close" class="e-icons" (click)='close()'></span>
            </div>
            <div class="content-area">
                <ejs-accordion #accordion [items]='data' (expanding)='expand($event)' (clicked)='clicked($event)'></ejs-accordion>
            </div>
        </ejs-sidebar>
        <!-- main content declaration -->
        <div>
            <div class="main-content">Main content</div>
        </div>`
})

export class AppComponent {
    @ViewChild('sidebar')
    private sidebarObj: SidebarComponent;
    @ViewChild('accordion')
    private accordionObj: AccordionComponent;

    private data: { [key: string]: Object }[] = [
        {
            header: 'Appliances',
            content: '<div id="Appliances_Items"></div>',
            subItems: [
                {
                    header: 'Kitchen',
                    content: '<div id="Appliances_Kitchen_Items"></div>',
                    subItems: [
                        { header: 'Electric Cookers' },
                        { header: 'Coffee Makers' },
                        { header: 'Blenders' },
                    ]
                },
                {
                    header: 'Washing Machine',
                    content: '<div id="Appliances_Washing_Items"></div>',
                    subItems: [
                        { header: 'Fully Automatic' },
                        { header: 'Semi Automatic' }
                    ]
                },
                {
                    header: 'Air Conditioners',
                    content: '<div id="Appliances_Conditioners_Items"></div>',
                    subItems: [
                        { header: 'Inverter ACs' },
                        { header: 'Split ACs' },
                        { header: 'Window ACs' },
                    ]
                }
            ]
        },
        {
            header: 'Accessories',
            content: '<div id="Accessories_Items"></div>',
            subItems: [
                {
                    header: 'Mobile',
                    content: '<div id="Accessories_Mobile_Items"></div>',
                    subItems: [
                        { header: 'Headphones' },
                        { header: 'Memory Cards' },
                        { header: 'Power Banks' }
                    ]
                },
                {
                    header: 'Computer',
                    content: '<div id="Accessories_Computer_Items"></div>',
                    subItems: [
                        { header: 'Pendrives' },
                        { header: 'External Hard Disks' },
                        { header: 'Monitors' }
                    ]
                }
            ]
        },
        {
            header: 'Fashion',
            content: '<div id="Fashion_Items"></div>',
            subItems: [
                { header: 'Men' },
                { header: 'Women' }
            ]
        },
        {
            header: 'Home & Living',
            content: '<div id="Home_Living_Items"></div>',
            subItems: [
                { header: 'Furniture' },
                { header: 'Decor' }
            ]
        },
        {
            header: 'Entertainment',
            content: '<div id="Entertainment_Items"></div>',
            subItems: [
                { header: 'Televisions' },
                { header: 'Home Theatres' },
                { header: 'Gaming Laptops' }
            ]
        }
    ];

    //Expanding Event function for Accordion component.
    private expand(e: ExpandEventArgs): void {
        if (e.isExpanded) {
            if (e.element.getElementsByClassName('e-acrdn-content')[0].children[0].classList.contains('e-accordion')) {
                return;
            }
            //Initialize Nested Accordion component
            let nestAcrdn: Accordion = new Accordion({
                items: (<{ subItems: object[] }>e.item).subItems,
                expanding: this.expand,
                clicked: this.clicked
            });

            let elemId: string = e.element.getElementsByClassName('e-acrdn-content')[0].children[0].id;
            //Render initialized Nested Accordion component
            nestAcrdn.appendTo('#' + elemId);
        }
    }

    private clicked(e: AccordionClickArgs): void {
        if (!e.item && !(e.originalEvent.target as HTMLElement).closest('.e-acrdn-item').getElementsByClassName('e-tgl-collapse-icon').length) {
            this.sidebarObj.hide();
        }
    }

    private hamburgerClick(): void {
        this.sidebarObj.show();
        this.accordionObj.refresh();
    }

    private close(): void {
        this.sidebarObj.hide();
    }
}
```

{% endtab %}

## Mobile view

The following example demonstrates the use case of Menu in Mobile mode by using ListView component with hamburger.

{% tab template="menu/listview", sourceFiles="app/**/*.ts,listview.css", isDefaultActive=true %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { enableRipple, Animation, AnimationOptions } from '@syncfusion/ej2-base';
import { ListViewComponent, SelectEventArgs } from '@syncfusion/ej2-angular-lists';

enableRipple(true);

@Component({
    selector: 'app-root',
    template: `<div class="layoutWrapper">
            <div class="speaker">
                <div class="camera"></div>
            </div>
            <div class="layout">
                <div id="container">
                    <div id="header">
                        <span id="hamburger" (click)="hamburgerClick()" class="e-icons menu default"></span>
                        <div class="content">Header</div>
                    </div>
                    <!-- ListView element -->
                    <ejs-listview  id="listview" #listview [dataSource]="dataSource" headerTitle="Menu" [showHeader]="true" (select)="onSelect($event)" tabindex="1" [style.display]='listViewDisplay' ></ejs-listview>
                    <span id="close" (click)="onClick($event)" class="e-icons" [style.display]='closeSpanDisplay'></span>
                </div>
            </div>
            <div class="outerButton"> </div>
        </div>`
})

export class AppComponent {
  @ViewChild('listview')
  private listObj: ListViewComponent;
  private listViewDisplay: string = 'none';
  private closeSpanDisplay: string = 'none';

  private dataSource: { [key: string]: Object }[] = [
    {
      text: 'Appliances',
      id: 'list1',
      child: [
        {
          text: 'Kitchen',
          id: 'list1_1',
          child: [
            { id: 'list1_1_1', text: 'Electric Cookers' },
            { id: 'list1_1_2', text: 'Coffee Makers' },
            { id: 'list1_1_3', text: 'Blenders' },
          ]
        },
        {
          text: 'Washing Machine',
          id: 'list1_2',
          child: [
            { id: 'list1_2_1', text: 'Fully Automatic' },
            { id: 'list1_2_2', text: 'Semi Automatic' }
          ]
        },
        {
          text: 'Air Conditioners',
          id: 'list1_3',
          child: [
            { id: 'list1_3_1', text: 'Inverter ACs' },
            { id: 'list1_3_2', text: 'Split ACs' },
            { id: 'list1_3_3', text: 'Window ACs' },
          ]
        }
      ]
    },
    {
      text: 'Accessories',
      id: 'list2',
      child: [
        {
          text: 'Mobile',
          id: 'list2_1',
          child: [
            { id: 'list2_1_1', text: 'Headphones' },
            { id: 'list2_1_2', text: 'Memory Cards' },
            { id: 'list2_1_3', text: 'Power Banks' }
          ]
        },
        {
          text: 'Computer',
          id: 'list2_2',
          child: [
            { id: 'list2_2_1', text: 'Pendrives' },
            { id: 'list2_2_2', text: 'External Hard Disks' },
            { id: 'list2_2_3', text: 'Monitors' }
          ]
        }
      ]
    },
    {
      text: 'Fashion',
      id: 'list3',
      child: [
        { id: 'list3_1', text: 'Men' },
        { id: 'list3_2', text: 'Women' }
      ]
    },
    {
      text: 'Home & Living',
      id: 'list4',
      child: [
        { id: 'list4_1', text: 'Furniture' },
        { id: 'list4_2', text: 'Decor' }
      ]
    },
    {
      text: 'Entertainment',
      id: 'list5',
      child: [
        { id: 'list5_1', text: 'Televisions' },
        { id: 'list5_2', text: 'Home Theatres' },
        { id: 'list5_3', text: 'Gaming Laptops' }
      ]
    }
  ];

  private onSelect(e: SelectEventArgs): void {
    if (e.data && !(e.data as { child: object }).child) {
      this.listViewDisplay = 'none';
      this.closeSpanDisplay = 'none';
      this.listObj.refresh();
    }
  }

  private onClick = (): void => {
    this.listViewDisplay = 'none';
    this.closeSpanDisplay = 'none';
  };

  private hamburgerClick = (): void => {
    let animation: Animation = new Animation({ duration: 500 });
    animation.animate(this.listObj.element, {
      name: 'SlideDown',
      begin: (args: AnimationOptions) => {
        this.listViewDisplay = 'block';
        this.closeSpanDisplay = 'block';
      }
    });
  };
}
```

{% endtab %}