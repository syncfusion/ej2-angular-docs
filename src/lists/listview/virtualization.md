---
title: "ListView UI Virtualization"
component: "ListView"
description: "Angular listView allows UI virtualization by loading viewable items in view port to improves listview performance when loading large data."
---

# UI Virtualization

UI virtualization loads only viewable list items in a view port which will increase ListView performance
on loading large number of data.

## Module injection

In order to use UI Virtualization, we need to import `VirtualizationService` module in the AppModule
and it should be injected to the provider section as follow

```typescript

import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent } from './app.component';
import { ListViewModule, VirtualizationService } from '@syncfusion/ej2-angular-lists';

/**
 * Module
 */
@NgModule({
    imports: [
        BrowserModule,
        ListViewModule
    ],
    declarations: [AppComponent],
    bootstrap: [AppComponent],
    providers: [VirtualizationService]
})
export class AppModule { }

```

## Getting started

UI virtualization can be enabled in ListView by setting `enableVirtualization` property to true.

It has two type of scroller

**Window scroll** - This scroller is used in ListView by default.

**Container scroll** - This will be used, if the height property of ListView was set.

{% tab template="listview/virtualization/flat-list", isDefaultActive = "true", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'my-app',
    template: `<ejs-listview id='ui-list' [dataSource]='listData' [enableVirtualization]='true' ></ejs-listview>`
})

export class AppComponent {
    public listData: { [key: string]: string | object }[] = [
        { text: 'Nancy', id: '0', },
        { text: 'Andrew', id: '1' },
        { text: 'Janet', id: '2' },
        { text: 'Margaret', id: '3' },
        { text: 'Steven', id: '4' },
        { text: 'Laura', id: '5' },
        { text: 'Robert', id: '6' },
        { text: 'Michael', id: '7' },
        { text: 'Albert', id: '8' },
        { text: 'Nolan', id: '9' }
    ];

    public ngOnInit() {
        for (let i: number = 10; i <= 1010; i++) {
            let index: number = parseInt((Math.random() * 10).toString());
            this.listData.push({ text: this.listData[index].text, id: i.toString() });
        }
    }
}

```

{% endtab %}

We can use `ng-template` property to customize list items in UI virtualization.

{% tab template="listview/virtualization/template", isDefaultActive = "true", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'my-app',
    template: `<ejs-listview id='ui-list' [dataSource]='listData' [enableVirtualization]='true' [height]=500 headerTitle='Contacts' [showHeader]='true'>
    <ng-template #template let-data="">
        <div class="list-container">
        <div id="icon" *ngIf="data.icon !== ''" class={{data.icon}}>
            <span class="showUI">{{data.icon}}</span>
            <img class="hideUI" width = '45' height = '45' src={{data.imgUrl}} />
        </div>
        <div id="icon" *ngIf="data.imgUrl !== ''" class="img">
            <span class="hideUI">{{data.icon}}</span>
            <img class="showUI" width = '45' height = '45' src={{data.imgUrl}} />
        </div>
        <div class="name">{{data.name}}</div>
        </div>
  </ng-template>
  </ejs-listview>`
})

export class AppComponent {
   public listData: { [key: string]: string | object }[] = [
    { name: 'Nancy', icon: 'N', imgUrl:'', id: '0', },
    { name: 'Andrew', icon: 'A', imgUrl:'', id: '1' },
    { name: 'Janet', icon: 'J', imgUrl:'', id: '2' },
    { name: 'Margaret', icon: '', imgUrl: 'https://ej2.syncfusion.com/demos/src/grid/images/2.png', id: '3' },
    { name: 'Steven', icon: 'S', imgUrl:'', id: '4' },
    { name: 'Laura', icon: '', imgUrl: 'https://ej2.syncfusion.com/demos/src/grid/images/3.png', id: '5' },
    { name: 'Robert', icon: 'R', imgUrl:'', id: '6' },
    { name: 'Michael', icon: 'M', imgUrl:'', id: '7' },
    { name: 'Albert', icon: '', imgUrl: 'https://ej2.syncfusion.com/demos/src/grid/images/5.png', id: '8' },
    { name: 'Nolan', icon: 'N', imgUrl:'', id: '9' }
];

public ngOnInit() {
    for (let i: number = 10; i <= 1010; i++) {
        let index: number = parseInt((Math.random() * 10).toString());
        this.listData.push({ name: this.listData[index].name, icon: this.listData[index].icon, imgUrl: this.listData[index].imgUrl, id: i.toString() });
    }
}
}

```

{% endtab %}
