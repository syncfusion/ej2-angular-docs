---
title: "Customization"
component: "File Manager"
description: "Customizing File Manager functionalities"
---

# Customizing File Manager functionalities

The file manager component allows customizing its functionalities like, context menu, searching, uploading, toolbar using APIs. Given below are some of the functionalities that can be customized in the File Manager,

* [Context menu customization](#context-menu-customization)
* [Details view customization](#details-view-customization)
* [Navigation pane customization](#navigation-pane-customization)
* [Show/Hide file extension](#showhide-file-extension)
* [Show/Hide hidden items](#showhide-hidden-items)
* [Show/Hide thumbnail images in large icons view](#showhide-thumbnail-images-in-large-icons-view)
* [Toolbar customization](#toolbar-customization)
* [Upload customization](#upload-customization)
* [Tooltip customization](#tooltip-customization)

## Context menu customization

The context menu settings like, items to be displayed on files, folders and layout click and visibility can be customized using [contextMenuSettings](../api/file-manager/#contextmenusettings) property.

{% tab template="file-manager/context-menu", isDefaultActive = "true",sourceFiles="app/**/*.ts,app/app.component.html" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    styleUrls: ['app/app.component.css'],
    templateUrl: 'app/app.component.html'
})
export class AppComponent {
    public ajaxSettings: object;
    public contextMenuSettings: object;
    public hostUrl: string = 'https://ej2-aspcore-service.azurewebsites.net/';
    public ngOnInit(): void {
        this.ajaxSettings = {
            url: this.hostUrl + 'api/FileManager/FileOperations',
            getImageUrl: this.hostUrl + 'api/FileManager/GetImage',
            uploadUrl: this.hostUrl + 'api/FileManager/Upload',
            downloadUrl: this.hostUrl + 'api/FileManager/Download'
        };
        // Context Menu settings customization
        this.contextMenuSettings = { file: ['Open', '|', 'Details'], folder: ['Open', '|', 'Details'], layout: ['SortBy', 'View', 'Refresh', '|', 'Details', '|'], visible: true};
    };
}

```

{% endtab %}

## Details view customization

The details view settings like, column width, header text, template for each field can be customized using [detailsViewSettings](../api/file-manager/#detailsviewsettings) property.

{% tab template="file-manager/detailsview", isDefaultActive = "true",sourceFiles="app/**/*.ts,app/app.component.html" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    styleUrls: ['app/app.component.css'],
    templateUrl: 'app/app.component.html'
})
export class AppComponent {
    public ajaxSettings: object;
    public view: string;
    public detailsViewSettings: object;
    public hostUrl: string = 'https://ej2-aspcore-service.azurewebsites.net/';
    public ngOnInit(): void {
        this.ajaxSettings = {
            url: this.hostUrl + 'api/FileManager/FileOperations',
            getImageUrl: this.hostUrl + 'api/FileManager/GetImage',
            uploadUrl: this.hostUrl + 'api/FileManager/Upload',
            downloadUrl: this.hostUrl + 'api/FileManager/Download'
        };
        // Initial view of File Manager is set to details view
        this.view = "Details";
        // Details View settings customization
        this.detailsViewSettings = {
            columns: [
                {field: 'name', headerText: 'File Name', minWidth: 120, width: 'auto', customAttributes: { class: 'e-fe-grid-name' },template: '${name}'},
                {field: 'size', headerText: 'File Size',minWidth: 50, width: '110', template: '${size}'},
                    { field: '_fm_modified', headerText: 'Date Modified',minWidth: 50, width: '190'}
            ]
        };
    };
}

```

{% endtab %}

## Navigation pane customization

The navigation pane settings like, minimum and maximum width and visibility can be customized using [navigationPaneSettings](../api/file-manager/#navigationpanesettings) property.

{% tab template="file-manager/navigationpane", isDefaultActive = "true",sourceFiles="app/**/*.ts,app/app.component.html" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    styleUrls: ['app/app.component.css'],
    templateUrl: 'app/app.component.html'
})
export class AppComponent {
    public ajaxSettings: object;
    public navigationPaneSettings: object;
    public hostUrl: string = 'https://ej2-aspcore-service.azurewebsites.net/';
    public ngOnInit(): void {
        this.ajaxSettings = {
            url: this.hostUrl + 'api/FileManager/FileOperations',
            getImageUrl: this.hostUrl + 'api/FileManager/GetImage',
            uploadUrl: this.hostUrl + 'api/FileManager/Upload',
            downloadUrl: this.hostUrl + 'api/FileManager/Download'
        };
        // Navigation Pane settings customization
        this.navigationPaneSettings = { maxWidth: '850px', minWidth: '140px', visible: true};
    };
}

```

{% endtab %}

## Show/Hide file extension

The file extensions are displayed in the File Manager by default. This can be hidden by disabling the [showFileExtension](../api/file-manager/#showfileextension) property.

In File Manager [fileLoad](../api/file-manager/#fileload) and [fileOpen](../api/file-manager/#fileopen) events are triggered before the file/folder is rendered and before the file/folder is opened respectively. These events can be utilized to perform operations before a file/folder is rendered or opened.

{% tab template="file-manager/fileextension", isDefaultActive = "true",sourceFiles="app/**/*.ts,app/app.component.html" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    styleUrls: ['app/app.component.css'],
    templateUrl: 'app/app.component.html'
})
export class AppComponent {
    public ajaxSettings: object;
    public showFileExtension: boolean;
    public hostUrl: string = 'https://ej2-aspcore-service.azurewebsites.net/';
    public ngOnInit(): void {
        this.ajaxSettings = {
            url: this.hostUrl + 'api/FileManager/FileOperations',
            getImageUrl: this.hostUrl + 'api/FileManager/GetImage',
            uploadUrl: this.hostUrl + 'api/FileManager/Upload',
            downloadUrl: this.hostUrl + 'api/FileManager/Download'
        };
        // Hides the file extension in File Manager
        this.showFileExtension = false;
    };
    // File Manager's file beforeFileLoad function
    onBeforeFileLoad(args: any) {
        console.log(args.fileDetails.name + " is loading");
    }
    // File Manager's file beforeFileOpen function
    onBeforeFileOpen(args: any) {
        console.log(args.fileDetails.name + " is opened");
    }
}

```

{% endtab %}

## Show/Hide hidden items

The File Manager provides support to show/hide the hidden items by enabling/disabling the [showHiddenItems](../api/file-manager/#showhiddenitems) property.

{% tab template="file-manager/hiddenitems", isDefaultActive = "true",sourceFiles="app/**/*.ts,app/app.component.html" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    styleUrls: ['app/app.component.css'],
    templateUrl: 'app/app.component.html'
})
export class AppComponent {
    public ajaxSettings: object;
    public showHiddenItems: boolean;
    public hostUrl: string = 'https://ej2-aspcore-service.azurewebsites.net/';
    public ngOnInit(): void {
        this.ajaxSettings = {
            url: this.hostUrl + 'api/FileManager/FileOperations',
            getImageUrl: this.hostUrl + 'api/FileManager/GetImage',
            uploadUrl: this.hostUrl + 'api/FileManager/Upload',
            downloadUrl: this.hostUrl + 'api/FileManager/Download'
        };
        // The default value set for showHiddenItems is false
        this.showHiddenItems = true;
    };
}

```

{% endtab %}

## Show/Hide thumbnail images in large icons view

The thumbnail images are displayed in the File Manager's large icons view by default. This can be hidden by disabling the [showThumbnail](../api/file-manager/#showthumbnail) property.

{% tab template="file-manager/disablethumbnail", isDefaultActive = "true",sourceFiles="app/**/*.ts,app/app.component.html" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    styleUrls: ['app/app.component.css'],
    templateUrl: 'app/app.component.html'
})
export class AppComponent {
    public ajaxSettings: object;
    public showThumbnail: boolean;
    public hostUrl: string = 'https://ej2-aspcore-service.azurewebsites.net/';
    public ngOnInit(): void {
        this.ajaxSettings = {
            url: this.hostUrl + 'api/FileManager/FileOperations',
            getImageUrl: this.hostUrl + 'api/FileManager/GetImage',
            uploadUrl: this.hostUrl + 'api/FileManager/Upload',
            downloadUrl: this.hostUrl + 'api/FileManager/Download'
        };
        // Hides the thumbnail images in File Manager's large icons view
        this.showThumbnail = false;
    };
}

```

{% endtab %}

## Toolbar customization

The toolbar settings like, items to be displayed in toolbar and visibility can be customized using [toolbarSettings](../api/file-manager/#toolbarsettings) property.

{% tab template="file-manager/toolbar-customize", isDefaultActive = "true",sourceFiles="app/**/*.ts,app/app.component.html" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    styleUrls: ['app/app.component.css'],
    templateUrl: 'app/app.component.html'
})
export class AppComponent {
    public ajaxSettings: object;
    public toolbarSettings: object;
    public hostUrl: string = 'https://ej2-aspcore-service.azurewebsites.net/';
    public ngOnInit(): void {
        this.ajaxSettings = {
            url: this.hostUrl + 'api/FileManager/FileOperations',
            getImageUrl: this.hostUrl + 'api/FileManager/GetImage',
            uploadUrl: this.hostUrl + 'api/FileManager/Upload',
            downloadUrl: this.hostUrl + 'api/FileManager/Download'
        };
        // Toolbar settings customization
        this.toolbarSettings = { items: ['NewFolder', 'Refresh', 'View', 'Details'], visible: true};
    };
}

```

{% endtab %}

## Upload customization

The upload settings like, minimum and maximum file size and enabling auto upload can be customized using [uploadSettings](../api/file-manager/#uploadsettings) property.

{% tab template="file-manager/upload", isDefaultActive = "true",sourceFiles="app/**/*.ts,app/app.component.html" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    styleUrls: ['app/app.component.css'],
    templateUrl: 'app/app.component.html'
})
export class AppComponent {
    public ajaxSettings: object;
    public uploadSettings: object;
    public hostUrl: string = 'https://ej2-aspcore-service.azurewebsites.net/';
    public ngOnInit(): void {
        this.ajaxSettings = {
            url: this.hostUrl + 'api/FileManager/FileOperations',
            getImageUrl: this.hostUrl + 'api/FileManager/GetImage',
            uploadUrl: this.hostUrl + 'api/FileManager/Upload',
            downloadUrl: this.hostUrl + 'api/FileManager/Download'
        };
        // Upload settings customization
        this.uploadSettings = { maxFileSize: 233332, minFileSize: 120, autoUpload: true};
    };
}

```

{% endtab %}

## Tooltip customization

The tooltip value can be customized by adding extra content to the title of the toolbar, navigation pane, details view and large icons of the file manager element.

{% tab template="file-manager/tooltip", isDefaultActive = "true",sourceFiles="app/**/*.ts,app/app.component.html" %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { FileManagerComponent, FileLoadEventArgs} from '@syncfusion/ej2-angular-filemanager';
import { TooltipComponent, TooltipEventArgs } from '@syncfusion/ej2-angular-popups';
import { getValue, select } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    styleUrls: ['app/app.component.css'],
    templateUrl: 'app/app.component.html'
})
export class AppComponent {
    @ViewChild('fileObj',{ static: true })
    public fileObj: FileManagerComponent;
    public ajaxSettings: object;
    public hostUrl: string = 'https://ej2-aspcore-service.azurewebsites.net/';
    public ngOnInit(): void {
        this.ajaxSettings = {
            url: this.hostUrl + 'api/FileManager/FileOperations',
            getImageUrl: this.hostUrl + 'api/FileManager/GetImage',
            uploadUrl: this.hostUrl + 'api/FileManager/Upload',
            downloadUrl: this.hostUrl + 'api/FileManager/Download'
        };
       };

    fileLoad (args: FileLoadEventArgs) {
        //Native tooltip customization to display additonal information in new line
        let target: Element = args.element;
        if (args.module==='DetailsView') {
            let element: Element = select('[title]', args.element);
            let title: string = getValue('name', args.fileDetails) +
                '\n' + getValue('dateModified', args.fileDetails);
            element.setAttribute('title', title);
        } else if (args.module==='LargeIconsView') {
            let title: string = getValue('name', args.fileDetails) +
                '\n' + getValue('dateModified', args.fileDetails);
            target.setAttribute('title', title);
        }
    }
}

```

{% endtab %}
