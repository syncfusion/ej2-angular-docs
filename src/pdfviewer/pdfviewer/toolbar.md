---
title: "Toolbar"
component: "PDF Viewer"
description: "Learn about the built-in Toolbar in PDF Viewer."
---

# Built-in toolbar

The PDF Viewer comes with a powerful built-in toolbar to execute important actions such as page navigation, text search,view mode,download,print,bookmark, and thumbnails.

The following table shows built-in toolbar items and its actions:-

| Option | Description |
|---|---|
| OpenOption | This option provides an action to load the PDF documents to the PDF Viewer.|
| PageNavigationTool |This option provides an action to navigate the pages in the PDF Viewer.
It contains GoToFirstPage,GoToLastPage,GotoPage,GoToNext, and GoToLast tools.|
| MagnificationTool |This option provides an action to magnify the pages either with predefined or user
defined zoom factors in the PDF Viewer. Contains ZoomIn, ZoomOut, Zoom, FitPage and FitWidth tools|
| PanTool |This option provides an action for panning the pages in the PDF Viewer.|
| SelectionTool |This option provides an action to enable/disable the text selection in the PDF Viewer.|
| SearchOption |This option provides an action to search a word in the PDF documents.|
| PrintOption |This option provides an action to print the PDF document being loaded in the PDF Viewer.|
| DownloadOption |This Download option provides an action to download the PDF document that has been loaded in the PDF Viewer.|
| UndoRedoTool | This tool provides options to undo and redo the annotation actions performed in the PDF Viewer.|
| AnnotationEditTool | This tool provides options to enable or disable the edit mode of annotation in the PDF Viewer.|

## Show/Hide the default toolbar

The PDF Viewer has an option to show or hide the complete default toolbar. You can achieve this by using following two ways.,

* **Show/Hide toolbar using enableToolbar API as in the following code snippet**

```typescript
    import { Component, OnInit } from '@angular/core';
import {
  LinkAnnotationService, BookmarkViewService, MagnificationService, ThumbnailViewService,
  ToolbarService, NavigationService, TextSearchService, AnnotationService, TextSelectionService, PrintService
} from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-container',
  // specifies the template string for the PDF Viewer component
  template: `<div class="content-wrapper">
  <ejs-pdfviewer id="pdfViewer" [serviceUrl]='service' [documentPath]='document' [enableToolbar]='true' style="height:640px;display:block"></ejs-pdfviewer>
</div>`,
  providers: [LinkAnnotationService, BookmarkViewService, MagnificationService,
    ThumbnailViewService, ToolbarService, NavigationService, AnnotationService, TextSearchService, TextSelectionService,PrintService]
})
export class AppComponent implements OnInit {
    public service = 'https://ej2services.syncfusion.com/production/web-services/api/pdfviewer';
    public document = 'PDF_Succinctly.pdf';
    ngOnInit(): void {
    }
}
```

* **Show/Hide toolbar using showToolbar as in the following code snippet**

```html
    <script>
       window.onload = function () {
            var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];
            pdfViewer.toolbar.showToolbar(false);
        }
    </script>
```

## Show/Hide the default toolbaritem

The PDF Viewer has an option to show or hide these grouped items in the default toolbar.

* **Show/Hide toolbaritem using toolbarSettings as in the following code snippet.**

```typescript
import { Component, OnInit } from '@angular/core';
import {
  LinkAnnotationService, BookmarkViewService, MagnificationService, ThumbnailViewService,
  ToolbarService, NavigationService, TextSearchService, AnnotationService, TextSelectionService, PrintService
} from '@syncfusion/ej2-angular-pdfviewer';

@Component({
  selector: 'app-container',
  // specifies the template string for the PDF Viewer component
  template: '<div class="content-wrapper">
  <ejs-pdfviewer id="pdfViewer" [serviceUrl]='service' [documentPath]='document' [toolbarSettings]='toolbarSettings'
    style="height:640px;display:block"></ejs-pdfviewer>
  </div>',
  providers: [LinkAnnotationService, BookmarkViewService, MagnificationService, ThumbnailViewService,
    ToolbarService, NavigationService, TextSearchService, AnnotationService, TextSelectionService,PrintService]
})
export class AppComponent implements OnInit {
    public service = 'https://ej2services.syncfusion.com/production/web-services/api/pdfviewer';
    public document = 'PDF_Succinctly.pdf';
    public toolbarSettings = { showTooltip: true, toolbarItem: 'DownloadOption' }
    ngOnInit(): void {
    }
}
```

* **Show/Hide toolbaritem using showToolbaritem as in the following code snippet**

```html
    <script>
       window.onload = function () {
            var pdfViewer = document.getElementById('pdfviewer').ej2_instances[0];
            pdfViewer.toolbar.showToolbarItem(new Array("DownloadOption"),true);
        }
    </script>
```

## See also

* [Toolbar customization](./how-to/toolbar_customization)
* [Feature Modules](./feature-module)