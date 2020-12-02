---
title: "ListView Customizing Templates"
component: "ListView"
description: "Angular listView allows customization of list item, header, and category group header using template and group header API."
---

# Customizing templates

The ListView component is designed to customize list items, group title and header title.

## Header template

ListView header can be customized with the help of the [`headerTemplate`](../api/list-view#headertemplate) property.

To customize header template in your application, set your customized template element inside ng tag directive along with [`showHeader`](../api/list-view#showheader) property as `true` to display the ListView header.

In the following example, we have rendered Listview with customized header which contains search, add and sort buttons.

{% tab template="listview/headerTemplate", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript

import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'my-app',
    template: `
    <div id = 'flat-list'>
        <!-- ListView element -->
        <ejs-listview id='element' [dataSource]='data' showHeader='true'>
            <ng-template #headerTemplate let-data="">
                <div class="headerContainer"><span class="fruitHeader">Fruits</span><button ejs-button id="search" iconCss='e-icons e-search-icon' cssClass='e-small e-round' isPrimary='true'></button><button ejs-button id="add" iconCss='e-icons e-add-icon' cssClass='e-small e-round' isPrimary='true'></button><button ejs-button id="sort" iconCss='e-icons e-sort-icon' cssClass='e-small e-round' isPrimary='true'></button></div>
            </ng-template>
        </ejs-listview>
    </div>
        `,
  })

export class AppComponent {

  public data=[
    { text: 'Date', id: '1', imgUrl: './dates.jpg' },
    { text: 'Fig', id: '2', imgUrl: './fig.jpg' },
    { text: 'Apple', id: '3', imgUrl: './apple.png' },
    { text: 'Apricot', id: '4', imgUrl: './apricot.jpg' },
    { text: 'Grape', id: '5', imgUrl: './grape.jpg' },
    { text: 'Strawberry', id: '6', imgUrl: './strawberry.jpg' },
    { text: 'Pineapple', id: '7', imgUrl: './pineapple.jpg' },
    { text: 'Melon', id: '8', imgUrl: './melon.jpg' },
    { text: 'Lemon', id: '9', imgUrl: './lemon.jpg' },
    { text: 'Cherry', id: '10', imgUrl: './cherry.jpg' },
    ];

}

```

{% endtab %}

## Template

ListView items can be customized with the help of the [`template`](../api/list-view#template) property.

To customize list items in your application, set your customized template element inside ng tag directive.

We provided the following built-in CSS classes to customize the list-items. Refer to the following table.

| CSS class        | Description           |
| ------------- |-------------|
| e-list-template, e-list-wrapper | These classes are used to differentiate normal and template rendering, which are mandatory for template rendering. The `e-list-template` class should be added to the root of the ListView element and `e-list-wrapper` class should be added to the template element wrapper.
| e-list-content | This class is used to align list content and it should be added to the content element <br/><br/> `<div class="e-list-wrapper">`<br/><b>`<span class="e-list-content">ListItem</span>`</b> <br/>`</div>`|
| e-list-avatar | This class is used for avatar customization. It should be added to the template element wrapper. After adding it, we can customize our element with [Avatar](https://ej2.syncfusion.com/angular/documentation/avatar/getting-started) classes <br/><br/> `<div class="e-list-wrapper`<b>`e-list-avatar`</b>`">` <br/> <b>`<span class="e-avatar e-avatar-circle">MR</span>`</b><br/>`<span class="e-list-content">ListItem</span>`<br/>`</div>`|
| e-list-avatar-right | This class is used to align avatar to right side of the list item. It should be added to the template element wrapper. After adding it, we can customize our element with [Avatar](https://ej2.syncfusion.com/angular/documentation/avatar/getting-started) classes <br/><br/> `<div class="e-list-wrapper`<b>`e-list-avatar-right`</b>`">` <br/> `<span class="e-list-content">ListItem</span>`<br/><b>`<span class="e-avatar e-avatar-circle">MR</span>`</b><br/> `</div>`|
| e-list-badge | This class is used for badge customization .It should be added to the template element wrapper. After adding it, we can customize our element with [Badge](https://ej2.syncfusion.com/angular/documentation/badge/getting-started) classes <br/><br/> `<div class="e-list-wrapper`<b>`e-list-badge`</b>`">` <br/> `<span class="e-list-content">ListItem</span>`<br/><b>`<span class="e-badge e-badge-primary">MR</span>`</b><br/> `</div>`|
| e-list-multi-line | This class is used for multi-line customization. It should be added to the template element wrapper. After adding it, we can customize List item's header and description <br/><br/>`<div class="e-list-wrapper`<b>`e-list-multi-line`</b>`">` <br/> `<span class="e-list-content">ListItem</span>`<br/>`</div>`|
| e-list-item-header |This class is used to align a list header and it should be added to the header element along with the multi-line class <br/><br/> `<div class="e-list-wrapper`<b>`e-list-multi-line`</b>`">`<br/> <b>`<span class="e-list-item-header">ListItem Header</span>`</b><br/> `<span class="e-list-content">ListItem</span>`<br/>`</div>`|

In the following example, we have customized list items with built-in CSS classes.

{% tab template="listview/avatar-template", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'my-app',
    template: `
    <div id="sample">
        <ejs-listview id='List' [dataSource]='data' headerTitle='Contacts' cssClass='e-list-template' [showHeader]='true' sortOrder='Ascending'>
            <ng-template #template let-data="">
                <div class="e-list-wrapper e-list-multi-line e-list-avatar">
                    <span class="e-avatar e-avatar-circle" *ngIf="data.avatar !== ''">{{data.avatar}}</span>
                    <span class="{{data.pic}} e-avatar e-avatar-circle" *ngIf="data.pic !== '' "> </span>
                    <span class="e-list-item-header">{{data.text}}</span>
                    <span class="e-list-content">{{data.contact}}</span>
                </div>
            </ng-template>
        </ejs-listview>
    </div>
    `
})

export class AppComponent {
     // Listview datasource with avatar and image source fields
     public data: { [key: string]: Object; }[] = [
  {
    text: "Jenifer",
    contact: "(206) 555-985774",
    id: "1",
    avatar: "",
    pic: "pic01"
  },
  { text: "Amenda", contact: "(206) 555-3412", id: "2", avatar: "A", pic: "" },
  {
    text: "Isabella",
    contact: "(206) 555-8122",
    id: "4",
    avatar: "",
    pic: "pic02"
  },
  {
    text: "William ",
    contact: "(206) 555-9482",
    id: "5",
    avatar: "W",
    pic: ""
  },
  {
    text: "Jacob",
    contact: "(71) 555-4848",
    id: "6",
    avatar: "",
    pic: "pic04"
  },
  { text: "Matthew", contact: "(71) 555-7773", id: "7", avatar: "M", pic: "" },
  {
    text: "Oliver",
    contact: "(71) 555-5598",
    id: "8",
    avatar: "",
    pic: "pic03"
  },
  {
    text: "Charlotte",
    contact: "(206) 555-1189",
    id: "9",
    avatar: "C",
    pic: ""
  }
];

}

```

{% endtab %}

## Group template

ListView group header can be customized with the help of the [`groupTemplate`](../api/list-view#grouptemplate) property.

To customize the group template in your application, set your customized template element inside ng tag directive.

In the following example, we have grouped Listview based on the category. The category of each list item should be mapped with [`groupBy`](../api/list-view/fieldSettingsModel#groupby) field of the data. We have also displayed grouped list items count in the group list header.

{% tab template="listview/item-count", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript

import { Component} from '@angular/core';

@Component({
    selector: 'my-app',
    template: `<ejs-listview id='List' [dataSource]='dataSource' cssClass='e-list-template' [fields]='fields'>
      <ng-template #template let-dataSource="">
        <div class="e-list-wrapper e-list-multi-line e-list-avatar">
            <img class="e-avatar e-avatar-circle" src={{dataSource.image}} style="background:#BCBCBC" />
            <span class="e-list-item-header">{{dataSource.Name}}</span>
            <span class="e-list-content">{{dataSource.contact}}</span>
        </div>
      </ng-template>
  </ejs-listview>`
})

export class AppComponent {
    public dataSource: Object = [
        { Name: 'Nancy', contact:'(206) 555-985774', id: '1', image: 'https://ej2.syncfusion.com/demos/src/grid/images/1.png',  category: 'Experience'},
        { Name: 'Janet', contact: '(206) 555-3412', id: '2', image: 'https://ej2.syncfusion.com/demos/src/grid/images/3.png', category: 'Fresher' },
        { Name: 'Margaret', contact:'(206) 555-8122', id:'4', image: 'https://ej2.syncfusion.com/demos/src/grid/images/4.png', category: 'Experience' },
        { Name: 'Andrew ', contact:'(206) 555-9482', id: '5', image: 'https://ej2.syncfusion.com/demos/src/grid/images/2.png', category: 'Experience'},
        { Name: 'Steven', contact:'(71) 555-4848', id: '6', image: 'https://ej2.syncfusion.com/demos/src/grid/images/5.png', category: 'Fresher' },
        { Name: 'Michael', contact:'(71) 555-7773', id: '7', image: 'https://ej2.syncfusion.com/demos/src/grid/images/6.png', category: 'Experience' },
        { Name: 'Robert', contact:'(71) 555-5598', id: '8', image: 'https://ej2.syncfusion.com/demos/src/grid/images/7.png', category: 'Fresher' },
        { Name: 'Laura', contact:'(206) 555-1189', id: '9', image: 'https://ej2.syncfusion.com/demos/src/grid/images/8.png', category: 'Experience' },
    ];

    public fields: Object = { text: 'Name', groupBy: 'category' };
}

```

{% endtab %}