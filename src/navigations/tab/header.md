---
title: "Tab Header"
component: "Tab"
description: "This section explains how to create the Tab control header with different styles in an Angular application."
---

# Header

This section explains about modifying the style of Tab header, and configuring its icons and positions.

## Styles

You can customize header styles by adding predefined classes in the Tab root element. The pre-defined CSS class names are as follows:

* **e-fill**: The Selected Tab header background is set as solid fill.
* **e-background**: Tab header has a solid fill background, and the selected header has a highlighted border.
* **e-background e-accent**: Tab header has a solid fill background, and the selected header has a highlighted border with accent color.

> If the above custom style classes are not included in the root element, the default style is applied to the Tab items.

{% tab template="tab/header", sourceFiles="app/**/*.ts,header.html"  %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { DropDownListComponent, ChangeEventArgs } from '@syncfusion/ej2-dropdowns';
import { TabComponent } from '@syncfusion/ej2-angular-navigations';
import { enableRipple } from '@syncfusion/ej2-base';
/**
 * Adaptive Tab Component
 */

@Component({
    selector: 'app-container',
    // specifies the template url path
    templateUrl: './header.html'
    })
export class AppComponent {
    @ViewChild('headerStyles');
    @ViewChild('element') tabObj: TabComponent;
    @ViewChild('headerStyles') listObj: TabComponent;
    public headerData: Object[] = [
        { Id: 'header1', headerStyle: 'default', text: 'Default' },
        { Id: 'header2', headerStyle: 'fill', text: 'Fill'},
        { Id: 'header3', headerStyle: 'background',text: 'Background' },
        { Id: 'header4', headerStyle: 'accent', text: 'Accent' }
    ];
    public fields: Object = { text: 'text', value: 'headerStyle' };
    public height: string = '220px';
    public value: string = 'default';
    public onChange(ChangeEventArgs: any): void {
        this.removeStyleClass();
        if (this.listObj.value === 'fill') {
            this.tabObj.element.classList.add('e-fill');
        } else if (this.listObj.value === 'background') {
            this.tabObj.element.classList.add('e-background');
        } else if (this.listObj.value === 'accent') {
            this.tabObj.element.classList.add('e-background');
            this.tabObj.element.classList.add('e-accent');
        }
    }
    public removeStyleClass(args: any): void {
        this.tabObj.element.classList.remove('e-fill');
        this.tabObj.element.classList.remove('e-background');
        this.tabObj.element.classList.remove('e-accent');
    }
    @ViewChild('adaptiveTab');
    public headerText: Object = [{ 'text': 'Twitter' }, { 'text': 'Facebook' },{ 'text': 'WhatsApp' }];

}

```

{% endtab %}

## Icon positions

You can customize the position of the Tab header icons using the [`iconPosition`](../api/tab/header#iconposition) property.  This property depends on the header items [`iconCss`](../api/tab/header#iconcss) property.  By default, Tab header icon is placed on left position.  The position values are as follows:

* **Left**: Icon is placed on the left of the Tab header item.
* **Right**: Icon is placed on the right of the Tab header item.
* **Top**: Icon is placed on the top of the Tab header item.
* **Bottom**: Icon is placed on the bottom of the Tab header item.

{% tab template="tab/icon-position", sourceFiles="app/**/*.ts,index.css"  %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { DropDownListComponent, ChangeEventArgs } from '@syncfusion/ej2-dropdowns';
import { TabComponent } from '@syncfusion/ej2-angular-navigations';
import { enableRipple } from '@syncfusion/ej2-base';
/**
 * Adaptive Tab Component
 */

@Component({
    selector: 'app-container',
    // specifies the template url path
    template: ` <div id="wrapper" style='margin-top: 20px'><div id='content' style="margin: 0px auto">
          <div id="default" style="padding-top:20px;width:250px">
            <div class='row'>
                <div>
                    <label> Icon Position </label>
                </div><br/>
                <div>
                    <ejs-dropdownlist id='iconPosition' #iconPosition [dataSource]='positionData' (change)='onChange($event)' [value]='value' [fields]='fields' [popupHeight]='height'></ejs-dropdownlist>
                </div>
            </div>
        </div>
        <br/><div><ejs-tab id="element" #element>
                <e-tabitems>
                        <e-tabitem [header]='headerText[0]'>
                            <ng-template #content>
                                Twitter is an online social networking service that enables users to send and read short 140-character messages called "tweets".
                                Registered users can read and post tweets, but those who are unregistered can only read them. Users access Twitter
                                through the website interface, SMS or mobile device app Twitter Inc. is based in San Francisco and has more than 25
                                offices around the world. Twitter was created in March 2006 by Jack Dorsey, Evan Williams, Biz Stone, and Noah Glass
                                and launched in July 2006. The service rapidly gained worldwide popularity, with more than 100 million users posting
                                340 million tweets a day in 2012.The service also handled 1.6 billion search queries per day.
                            </ng-template>
                        </e-tabitem>
                        <e-tabitem [header]='headerText[1]'>
                            <ng-template #content>
                                Facebook is an online social networking service headquartered in Menlo Park, California. Its website was launched on February
                                4, 2004, by Mark Zuckerberg with his Harvard College roommates and fellow students Eduardo Saverin, Andrew McCollum,
                                Dustin Moskovitz and Chris Hughes.The founders had initially limited the website\'\s membership to Harvard students,
                                but later expanded it to colleges in the Boston area, the Ivy League, and Stanford University. It gradually added support
                                for students at various other universities and later to high-school students.
                            </ng-template>
                        </e-tabitem>
                        <e-tabitem [header]='headerText[2]'>
                            <ng-template #content>
                                WhatsApp Messenger is a proprietary cross-platform instant messaging client for smartphones that operates under a subscription
                                business model. It uses the Internet to send text messages, images, video, user location and audio media messages to
                                other users using standard cellular mobile numbers. As of February 2016, WhatsApp had a user base of up to one billion,[10]
                                making it the most globally popular messaging application. WhatsApp Inc., based in Mountain View, California, was acquired
                                by Facebook Inc. on February 19, 2014, for approximately US$19.3 billion.
                            </ng-template>
                        </e-tabitem>
                    </e-tabitems>
                </ejs-tab>
        </div>
      </div>
 </div>`
    })
export class AppComponent {
    @ViewChild('element') tabObj: TabComponent;
    @ViewChild('iconPosition') listObj: DropDownListComponent;
    public positionData: Object[] = [
        { position: 'left', text: 'Left' },
        { position: 'right', text: 'Right'},
        { position: 'top',text: 'Top' },
        { position: 'bottom', text: 'Bottom' }
    ];
    public fields: Object = { text: 'text', value: 'position' };
    public height: string = '220px';
    public value: string = 'left';
    public onChange(ChangeEventArgs: any): void {
          let items: any = this.tabObj.items;
          for(let i: number = 0; i < items.length; i++) {
             items[i].header.iconPosition = this.listObj.value;
          }
    }
    public headerText: Object = [{ 'text': 'Twitter', 'iconCss': 'e-twitter' }, { 'text': 'Facebook', 'iconCss': 'e-facebook' },{ 'text': 'WhatsApp', 'iconCss': 'e-whatsapp' }];

}

```

{% endtab %}

## See Also

* [How to customize selected tab styles](./how-to/customize-selected-tab-styles/)