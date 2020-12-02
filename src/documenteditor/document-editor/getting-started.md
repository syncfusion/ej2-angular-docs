---
title: "Getting Started"
component: "DocumentEditor"
description: "Learn how to get started using JavaScript document editor component through simple steps."
---

# Getting Started

This section explains the steps to create a Word document editor within your application and demonstrates the basic usage of the DocumentEditor component.

## Dependencies

The list of dependencies required to use the DocumentEditor component in your application is given below:

```javascript
|-- @syncfusion/ej2-angular-documenteditor
    |-- @syncfusion/ej2-angular-base
    |-- @syncfusion/ej2-documenteditor
    |-- @syncfusion/ej2-base
    |-- @syncfusion/ej2-buttons
    |-- @syncfusion/ej2-compression
    |-- @syncfusion/ej2-data
    |-- @syncfusion/ej2-dropdowns
    |-- @syncfusion/ej2-file-utils
    |-- @syncfusion/ej2-inputs
    |-- @syncfusion/ej2-lists
    |-- @syncfusion/ej2-navigations
    |-- @syncfusion/ej2-popups
    |-- @syncfusion/ej2-splitbuttons
    |-- @syncfusion/ej2-charts
```

## Setup your development environment

* To setup basic `Angular` sample use following commands.

```javascript
git clone https://github.com/angular/quickstart.git quickstart
cd quickstart
npm install
```

For more information, refer to [Angular sample setup](https://angular.io/guide/setup/)

* To install `DocumentEditor` packages using below command.

```javascript
npm install @syncfusion/ej2-angular-documenteditor --save
```

The above package installs `DocumentEditor dependencies` which are required to render the component in the Angular environment.

## Configuring system JS

[Syncfusion DocumentEditor packages](./getting-started#dependencies/) need to be mapped in systemjs.config.js configuration file.

Syncfusion `ej2-angular-documenteditor` packages have to be mapped in the systemjs.config.js configuration file.

```javascript
/**
 * System configuration for Angular samples
 * Adjust as necessary for your application needs.
 */
(function (global) {
  System.config({
    paths: {
      // paths serve as alias
      'npm:': 'node_modules/',
      'syncfusion:': './node_modules/@syncfusion/',
    },
    // map tells the System loader where to look for things
    map: {
        // our app is within the app folder
        'app': 'app',
        // angular bundles
        '@angular/core': 'npm:@angular/core/bundles/core.umd.js',
        '@angular/common': 'npm:@angular/common/bundles/common.umd.js',
        '@angular/compiler': 'npm:@angular/compiler/bundles/compiler.umd.js',
        '@angular/platform-browser': 'npm:@angular/platform-browser/bundles/platform-browser.umd.js',
        '@angular/platform-browser-dynamic': 'npm:@angular/platform-browser-dynamic/bundles/platform-browser-dynamic.umd.js',
        '@angular/http': 'npm:@angular/http/bundles/http.umd.js',
        '@angular/router': 'npm:@angular/router/bundles/router.umd.js',
        '@angular/forms': 'npm:@angular/forms/bundles/forms.umd.js',

        // syncfusion bundles
        "@syncfusion/ej2-base": "syncfusion:ej2-base/dist/ej2-base.umd.min.js",
        "@syncfusion/ej2-buttons": "syncfusion:ej2-buttons/dist/ej2-buttons.umd.min.js",
        "@syncfusion/ej2-splitbuttons": "syncfusion:ej2-splitbuttons/dist/ej2-splitbuttons.umd.min.js",
        "@syncfusion/ej2-data": "syncfusion:ej2-data/dist/ej2-data.umd.min.js",
        "@syncfusion/ej2-dropdowns": "syncfusion:ej2-dropdowns/dist/ej2-dropdowns.umd.min.js",
        "@syncfusion/ej2-inputs": "syncfusion:ej2-inputs/dist/ej2-inputs.umd.min.js",
        "@syncfusion/ej2-lists": "syncfusion:ej2-lists/dist/ej2-lists.umd.min.js",
        "@syncfusion/ej2-navigations": "syncfusion:ej2-navigations/dist/ej2-navigations.umd.min.js",
        "@syncfusion/ej2-compression": "syncfusion:ej2-compression/dist/ej2-compression.umd.min.js",
        "@syncfusion/ej2-popups": "syncfusion:ej2-popups/dist/ej2-popups.umd.min.js",
        "@syncfusion/ej2-file-utils": "syncfusion:ej2-file-utils/dist/ej2-file-utils.umd.min.js",
        "@syncfusion/ej2-office-chart": "syncfusion:ej2-office-chart/dist/ej2-office-chart.umd.min.js",
        "@syncfusion/ej2-calendars": "syncfusion:ej2-calendars/dist/ej2-calendars.umd.min.js",
        "@syncfusion/ej2-pdf-export": "syncfusion:ej2-pdf-export/dist/ej2-pdf-export.umd.min.js",
        "@syncfusion/ej2-svg-base": "syncfusion:ej2-svg-bases/dist/ej2-svg-base.umd.min.js",
        "@syncfusion/ej2-charts": "syncfusion:ej2-charts/dist/ej2-charts.umd.min.js",
        "@syncfusion/ej2-documenteditor": "syncfusion:ej2-documenteditor/dist/ej2-documenteditor.umd.min.js",
        "@syncfusion/ej2-angular-base": "syncfusion:ej2-angular-base/dist/ej2-angular-base.umd.min.js",

        "@syncfusion/ej2-angular-documenteditor": "syncfusion:ej2-angular-documenteditor/dist/ej2-angular-documenteditor.umd.min.js",
          // other libraries
        'rxjs':                      'npm:rxjs',
        'angular-in-memory-web-api': 'npm:angular-in-memory-web-api/bundles/in-memory-web-api.umd.js'
    },
    // packages tells the System loader how to load when no filename and/or no extension
    packages: {
      app: {
        defaultExtension: 'js',
        meta: {
          './*.js': {
            loader: 'systemjs-angular-loader.js'
          }
        }
      },
      rxjs: {
        defaultExtension: 'js'
      }
    }
  });
})(this);
```

## Adding CSS reference

 Combined CSS files are available in the Essential JS 2 package root folder.
This can be referenced in your [src/styles.css] using following code.

```css
@import '../node_modules/@syncfusion/ej2-base/styles/material.css';
@import '../node_modules/@syncfusion/ej2-buttons/styles/material.css';
@import '../node_modules/@syncfusion/ej2-inputs/styles/material.css';
@import '../node_modules/@syncfusion/ej2-popups/styles/material.css';
@import '../node_modules/@syncfusion/ej2-lists/styles/material.css';
@import '../node_modules/@syncfusion/ej2-navigations/styles/material.css';
@import '../node_modules/@syncfusion/ej2-splitbuttons/styles/material.css';
@import '../node_modules/@syncfusion/ej2-dropdowns/styles/material.css';
@import '../node_modules/@syncfusion/ej2-angular-documenteditor/styles/material.css';
```

## Adding Component -

You can add `DocumentEditorContainer` Component with  predefined toolbar and properties pane options or `DocumentEditor` component with customize options.

## DocumentEditor Component

DocumentEditor Component is used to create , view and edit word documents. In this , you can customize the UI options based on your requirements to modify the document.

### Registering DocumentEditor Module

Import DocumentEditor module into Angular application(app.module.ts) from the package `@syncfusion/ej2-angular-documenteditor` [src/app/app.module.ts].

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the DocumentEditorModule for the DocumentEditor component
import { DocumentEditorModule } from '@syncfusion/ej2-angular-documenteditor';
import { AppComponent }  from './app.component';

@NgModule({
  //declaration of ej2-angular-documenteditor module into NgModule
  imports:      [ BrowserModule, DocumentEditorModule ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

### Adding DocumentEditor component

Modify the template in [src/app/app.component.ts] file to render the DocumentEditor component.
Add the Angular DocumentEditor by using `<ejs-documenteditor>` selector in `template` section of the app.component.ts file.

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-container',
  // specifies the template string for the DocumentEditor component
  template: `<ejs-documenteditor serviceUrl="https://ej2services.syncfusion.com/production/web-services/api/documenteditor/"> </ejs-documenteditor>`
})
export class AppComponent implements OnInit {

    ngOnInit(): void {
    }
}

```

> The DocumentEditor requires server-side interactions for the following operations:
>
> * Paste with formatting
> * Restrict editing
> * Spellcheck
>
> Refer to this [link](https://github.com/SyncfusionExamples/EJ2-DocumentEditor-WebServices) to configure the web service and set the [serviceUrl](https://ej2.syncfusion.com/angular/documentation/api/document-editor#serviceurl).

### Run the  DocumentEditor application

The quickstart project is configured to compile and run the application in a browser. Use the following command to run the application.

```javascript
npm start
```

Output will be displayed as follows.

{% tab template="document-editor/getting-started",isDefaultActive=true, sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';
import {
    DocumentEditorComponent, PrintService, SfdtExportService, WordExportService, TextExportService, SelectionService,
    SearchService, EditorService, ImageResizerService, EditorHistoryService, ContextMenuService,
    OptionsPaneService, HyperlinkDialogService, TableDialogService, BookmarkDialogService, TableOfContentsDialogService,
    PageSetupDialogService, StyleDialogService, ListDialogService, ParagraphDialogService, BulletsAndNumberingDialogService,
    FontDialogService, TablePropertiesDialogService, BordersAndShadingDialogService, TableOptionsDialogService,
    CellOptionsDialogService, StylesDialogService
} from '@syncfusion/ej2-angular-documenteditor';

@Component({
    selector: 'app-container',
    template: `<ejs-documenteditor  id="container" serviceUrl="https://ej2services.syncfusion.com/production/web-services/api/documenteditor/" style="display:block;height:400px" [isReadOnly]=false [enableSelection]=true
    [enablePrint]=true [enableSfdtExport]=true [enableWordExport]=true [enableOptionsPane]=true [enableContextMenu]=true
    [enableHyperlinkDialog]=true [enableBookmarkDialog]=true [enableTableOfContentsDialog]=true [enableSearch]=true
    [enableParagraphDialog]=true [enableListDialog]=true [enableTablePropertiesDialog]=true [enableBordersAndShadingDialog]=true
    [enablePageSetupDialog]=true [enableStyleDialog]=true [enableFontDialog]=true [enableTableOptionsDialog]=true
    [enableTableDialog]=true [enableImageResizer]=true [enableEditor]=true [enableEditorHistory]=true>
    </ejs-documenteditor>`,
    encapsulation: ViewEncapsulation.None,
    providers: [PrintService, SfdtExportService, WordExportService, TextExportService, SelectionService, SearchService, EditorService,
    ImageResizerService, EditorHistoryService, ContextMenuService, OptionsPaneService, HyperlinkDialogService, TableDialogService,
    BookmarkDialogService, TableOfContentsDialogService, PageSetupDialogService, StyleDialogService, ListDialogService,
    ParagraphDialogService, BulletsAndNumberingDialogService, FontDialogService, TablePropertiesDialogService,
    BordersAndShadingDialogService, TableOptionsDialogService, CellOptionsDialogService, StylesDialogService]
})

export class AppComponent {

}

```

{% endtab %}

## DocumentEditorContainer Component

DocumentEditorContainer Component is also used to create, view and edit word document. But here, you can use predefined toolbar and properties pane to view and modify word document.

### Registering DocumentEditorContainer Module

Import DocumentEditorContainer module into Angular application(app.module.ts) from the package `@syncfusion/ej2-angular-documenteditor` [src/app/app.module.ts].

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { DocumentEditorContainerModule } from '@syncfusion/ej2-angular-documenteditor';
import { AppComponent } from './default.component';



/**
 * Module
 */
@NgModule({
    imports: [
        BrowserModule,
        DocumentEditorContainerModule
    ],
    declarations: [AppComponent],
    bootstrap: [AppComponent]
})
export class AppModule { }
```

### Adding DocumentEditorContainer component

Modify the template in [src/app/app.component.ts] file to render the DocumentEditorContainer component.
Add the Angular DocumentEditorContainer by using `<ejs-documenteditor>` selector in `template` section of the app.component.ts file.

```typescript
import { Component, OnInit } from '@angular/core';
import { ToolbarService } from '@syncfusion/ej2-angular-documenteditor';

@Component({
  selector: 'app-container',
  // specifies the template string for the DocumentEditorContainer component
  template: `<ejs-documenteditorcontainer serviceUrl="https://ej2services.syncfusion.com/production/web-services/api/documenteditor/" [enableToolbar]=true> </ejs-documenteditorcontainer>`,
  providers: [ToolbarService]
})
export class AppComponent implements OnInit {

  ngOnInit(): void {
  }
}

```

> The DocumentEditorContainer requires server-side interactions for the following operations:
>
> * Opening word documents
> * Paste with formatting
> * Restrict editing
> * Spellcheck
>
> Refer to this [link](https://github.com/SyncfusionExamples/EJ2-DocumentEditor-WebServices) to configure the web service and set the [serviceUrl](https://ej2.syncfusion.com/angular/documentation/api/document-editor-container#serviceurl).

### Run the DocumentEditorContainer application

The quickstart project is configured to compile and run the application in a browser. Use the following command to run the application.

```javascript
npm start
```

DocumentEditorContainer output will be displayed as follows.

{% tab template="document-editor/document-editor-container",isDefaultActive=true, sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { ToolbarService } from '@syncfusion/ej2-angular-documenteditor';
@Component({
  selector: 'app-container',
  // specifies the template string for the DocumentEditorContainer component
  template: `<ejs-documenteditorcontainer serviceUrl="https://ej2services.syncfusion.com/production/web-services/api/documenteditor/" style="display:block;height:600px" [enableToolbar]=true> </ejs-documenteditorcontainer>`,
  providers: [ToolbarService]
})
export class AppComponent implements OnInit {

  ngOnInit(): void {
  }
}

```

{% endtab %}