---
title: "How to"
component: "DocumentEditor"
description: "Learn how to customize the existing toolbar in document editor."
---

# Customize existing toolbar

## How to customize existing toolbar in DocumentEditorContainer

DocumentEditorContainer allows you to customize(add, show, hide, enable, and disable) existing items in a toolbar.

* Add - New items can defined by [`CustomToolbarItemModel`](../../api/document-editor/customToolbarItemModel/) and with existing items in [`toolbarItems`](../../api/document-editor-container/#toolbaritems) property. Newly added item click action can be defined in [`toolbarclick`](../../api/toolbar/clickEventArgs/).

* Show, Hide - Existing items can be shown or hidden using the [`toolbarItems`](../../api/document-editor-container/#toolbaritems) property. Pre-defined toolbar items are available with [`ToolbarItem`](../../api/document-editor/toolbarItem/).

* Enable, Disable -  Toolbar items can be enabled or disable using [`enableItems`](../../api/document-editor-container/toolbar/#enableitems)

```typescript
import { Component, ViewChild } from '@angular/core';
import { ClickEventArgs } from '@syncfusion/ej2-navigations'
import {  DocumentEditorContainerComponent, ToolbarService, CustomToolbarItemModel} from '@syncfusion/ej2-angular-documenteditor';

@Component({
  selector: 'app-root',
  template: '<ejs-documenteditorcontainer [toolbarItems]=items (toolbarClick)="onToolbarClick($event)" #documenteditor_default style="display:block;height:600px" [enableToolbar]=true></ejs-documenteditorcontainer>',
  styleUrls: ['./app.component.css'],
  providers: [ToolbarService]
})
export class AppComponent {  
  @ViewChild('documenteditor_default',{ static: true }) container: DocumentEditorContainerComponent;
  public toolItem: CustomToolbarItemModel = {
  prefixIcon: "e-de-ctnr-lock",
  tooltipText: "Disable Image",
  text: "Disable Image",
  id: "Custom"
  };
  public items = [this.toolItem,'Undo','Redo','Separator','Image','Table','Hyperlink','Bookmark','Comments','TableOfContents','Separator','Header','Footer','PageSetup','PageNumber','Break','Separator','Find','Separator','LocalClipboard','RestrictEditing'];
  public onToolbarClick(args:ClickEventArgs): void {
    switch(args.item.id){
        case 'Custom':
            //Disable image toolbar item.
            this.container.toolbar.enableItems(4, false);
            break;
    }
  };
}
```

>Note: Default value of `toolbarItems` is `['New', 'Open', 'Separator', 'Undo', 'Redo', 'Separator', 'Image', 'Table', 'Hyperlink', 'Bookmark', 'Comments', 'TableOfContents', 'Separator', 'Header', 'Footer', 'PageSetup', 'PageNumber', 'Break', 'Separator', 'Find', 'Separator', 'LocalClipboard', 'RestrictEditing']`.