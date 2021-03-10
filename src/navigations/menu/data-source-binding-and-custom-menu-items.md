---
title: "Menu with datasource and HTML tags"
component: "Menu"
description: "Typescript Menu supports HTML elements for menu items, databinding with local data source, parent child data, array of JSON data, and remote service with query."
---

# Data source binding and Custom menu items

## Data binding

The Menu supports data source bindings such as array of JavaScript objects
that can be structured as either `hierarchical` or `self-referential` data.

### Hierarchical data

The Menu can be populated with hierarchical data source by assigning it to the [`items`](../api/menu/menuItemModel#items)
property, and the fields with corresponding keys can be mapped to the
[`fields`](../api/menu/fieldSettingsModel) property.

#### JSON data

The Menu can generate its menu items through an array of complex data source by mapping fields
from the [`fields`](../api/menu/fieldSettingsModel) property.

{% tab template="menu/data-binding", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { enableRipple } from '@syncfusion/ej2-base';
import { FieldSettingsModel } from '@syncfusion/ej2-angular-navigations';

// Import an array of JSON data from datasource.ts
import { dataSource } from './datasource';

enableRipple(true);

@Component({
    selector: 'app-root',
    template: `<ejs-menu [items]="data" [fields]='menuFields'></ejs-menu>`
})

export class AppComponent {
    private menuFields: FieldSettingsModel = {
        text: ['continent', 'country', 'language'],
        children: ['countries', 'languages']
    };

    private data: { [key: string]: Object }[] = dataSource;
}
```

{% endtab %}

#### Data Service

In application level, remote data binding can be achieved using [`DataManager`](https://ej2.syncfusion.com/angular/documentation/data).
To create Menu, assign items property with resultant data from
[`callback`](https://ej2.syncfusion.com/documentation/api/data/deferred#then) function.

The following example displays five employees' **FirstName** from **Employees** table
and **ShipName** details from **Orders** table of the `Northwind` Data Service.

{% tab template="menu/data-service", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, OnInit } from '@angular/core';
import { enableRipple } from '@syncfusion/ej2-base';
import { DataManager, Query, ODataAdaptor, ReturnOption } from '@syncfusion/ej2-data';
import { FieldSettingsModel } from '@syncfusion/ej2-angular-navigations';

enableRipple(true);

@Component({
    selector: 'app-root',
    template: `<ejs-menu *ngIf='menuItems' [items]='menuItems' [fields]='menuFields'></ejs-menu>`
})

export class AppComponent implements OnInit {

    private SERVICE_URI: string = 'https://js.syncfusion.com/ejServices/Wcf/Northwind.svc/';

    // Menu fields definition.
    private menuFields: FieldSettingsModel = {
        text: ['FirstName', 'ShipName'],
        children: ['Orders']
    };

    private menuItems: { [key: string]: Object }[];

    public ngOnInit(): void {
        // Getting remote data using DataManager.
        new DataManager({ url: this.SERVICE_URI, adaptor: new ODataAdaptor, crossDomain: true })
            .executeQuery(
                new Query().from('Employees').take(5).hierarchy(
                    new Query()
                        .foreignKey('EmployeeID')
                        .from('Orders').take(13),
                    function () {
                        return [1, 2, 3, 4, 5]
                    }
                ))
            .then((e: ReturnOption) => {
                //Assign result data to menu items
                this.menuItems = e.result as { [key: string]: Object }[];
                document.getElementById('loader').style.display = "none";
            });
    }
}
```

{% endtab %}

### Self-referential data

Menu can be populated from self-referential data structure that contains array of JSON objects
with `parentId` mapping.

You can directly assign self-referential data to the [`items`](../api/menu/menuItemModel#items)
property, and map all the field members
with corresponding keys from self-referential data to [fields](../api/menu#fields) property.

To render the root level nodes, specify the `parentId` as null or no need to specify the `parentId` in data source.

In the following example, the **id**, **pId**, and **text** columns from self-referential data have been mapped to the [`itemId`](../api/menu/fieldSettingsModel/#itemid), [`parentId`](../api/menu/fieldSettingsModel/#parentid), and [`text`](../api/menu/fieldSettingsModel/#text) fields, respectively.

{% tab template="menu/getting-started", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { enableRipple } from '@syncfusion/ej2-base';
import { FieldSettingsModel } from '@syncfusion/ej2-angular-navigations';

enableRipple(true);

@Component({
    selector: 'app-root',
    template: `<ejs-menu [items]='data' [fields]='menuFields'></ejs-menu>`
})

export class AppComponent {
    //Menu datasource
    private data: { [key: string]: Object }[] = [
        { id: 'parent1', text: 'Events' },
        { id: 'parent2', text: 'Movies' },
        { id: 'parent3', text: 'Directory' },
        { id: 'parent4', text: 'Queries', pId: null },
        { id: 'parent5', text: 'Services', pId: null },

        { id: 'parent6', text: 'Conferences', pId: 'parent1' },
        { id: 'parent7', text: 'Music', pId: 'parent1' },
        { id: 'parent8', text: 'Workshops', pId: 'parent1' },

        { id: 'parent9', text: 'Now Showing', pId: 'parent2' },
        { id: 'parent10', text: 'Coming Soon', pId: 'parent2' },

        { id: 'parent10', text: 'Media Gallery', pId: 'parent3' },
        { id: 'parent11', text: 'Newsletters', pId: 'parent3' },

        { id: 'parent12', text: 'Our Policy', pId: 'parent4' },
        { id: 'parent13', text: 'Site Map', pId: 'parent4' },
        { id: 'parent14', text: 'Pop', pId: 'parent7' },
        { id: 'parent15', text: 'Folk', pId: 'parent7' },
        { id: 'parent16', text: 'Classical', pId: 'parent7' }
    ];

    //Menu fields definition
    private menuFields: FieldSettingsModel = {
        itemId: 'id',
        text: 'text',
        parentId: 'pId'
    };
}
```

{% endtab %}

## Custom menu items

The Menu can be customized using Essential JS2
[Template engine](https://ej2.syncfusion.com/documentation/common/template-engine) to render the elements.

To customize menu items in your application, set your customized template string to the
[`template`](../api/menu#template) property.
In the following example, the menu has been rendered with customized menu items.

{% tab template="menu/custom-menu-items", sourceFiles="app/**/*.ts,template.css", isDefaultActive=true %}

```typescript
import { Component, Inject } from '@angular/core';
import { FieldSettingsModel } from '@syncfusion/ej2-angular-navigations';
import { enableRipple } from '@syncfusion/ej2-base';

enableRipple(false);

@Component({
    selector: 'app-root',
    styleUrls: ['template.css'],
    template: `
    <div id="menuTemplate" class="menu-section">
    <div class="menu-control">
        <ejs-menu [items]='dataSource' [fields]='menuFields' [animationSettings]="animation" cssClass="e-template-menu">
            <ng-template #template let-dataSource="">
                {{dataSource.category}}
                <div *ngIf="dataSource.value" style="width:100%;display:flex;justify-content:space-between;">
                    <img *ngIf="dataSource.url" class="e-avatar e-avatar-small"
                        src="src/images/platforms/{{dataSource.url}}.png" />
                    <span style="width:100%;">{{dataSource.value}}</span>
                    <span *ngIf="dataSource.count" class='e-badge e-badge-success'>{{dataSource.count}}</span>
                </div>
                <div *ngIf="dataSource.about" tabindex="0" class="e-card">
                    <div class="e-card-header">
                        <div class="e-card-header-caption">
                            <div class="e-card-header-title">About Us</div>
                        </div>
                    </div>
                    <div class="e-card-content">
                        {{dataSource.about.value}}
                    </div>
                    <div class="e-card-actions">
                        <button class="e-btn e-outline" style="pointer-events: auto;">
                            Read More
                        </button>
                    </div>
                </div>
            </ng-template>
        </ejs-menu>
    </div>
</div>
    `
})

export class AppComponent {
      constructor(@Inject('sourceFiles') private sourceFiles: any) {
        sourceFiles.files = ['template.css'];
    }
    //Template datasource
    private dataSource: { [key: string]: Object }[] = [
     {
            category: 'Products',
            options: [
                { value: 'JavaScript', url: '../../../../../../menu/images/javascript' },
                { value: 'Angular', url: '../../../../../../menu/images/angular' },
                { value: 'ASP.NET Core', url: '../../../../../../menu/images/core' },
                { value: 'ASP.NET MVC', url: '../../../../../../menu/images/mvc' }
            ]
        },
        {
            category: 'Services',
            options: [
                { value: 'Application Development', count: '1200+' },
                { value: 'Maintenance & Support', count: '3700+' },
                { value: 'Quality Assurance' },
                { value: 'Cloud Integration', count: '900+' }
            ]
        },
        {
            category: 'About Us',
            options: [
                {
                    id: 'about',
                    about: {
                        value: "We are on a mission to provide world-class best software solutions for web, mobile and desktop platforms. Around 900+ applications are desgined and delivered to our customers to make digital & strengthen their businesses."
                    }
                }
            ]
        },
        { category: 'Careers' },
        { category: 'Sign In' }
    ];

    // Menu fields definition
    private menuFields: object = {
        text: ['category', 'value'],
        children: ['options']
    };
}
```

{% endtab %}

>To prevent sub menu closing, set `args.cancel` to `true` in [`beforeClose`](../api/menu#beforeclose) event.

## See Also

* [Render menu with items](./getting-started#getting-started)