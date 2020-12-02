---
title: "Rich Text Editor Inline editing mode"
component: "Rich Text Editor"
description: "This section for Syncfusion's Angular Rich Text Editor component demonstrates on how to enable the inline mode editor on demand while editing the content."
---

# Inline Mode

This is the inline example for the Rich Text Editor. For this you must set the [`inlineMode`](../api/rich-text-editor/#inlinemode) property.

Inline edition allows you to select any editable element or click the element on the page and edit it in-place.

Inline editing is a true WYSIWYG formation and on the contrary to Rich Text Editor HTML/MD editing, the styles that are used for edited content comes directly from the document stylesheet. This means that inline editors ignore the default Rich Text Editor content styles.

## Show on select/click

Enabling the [`onSelection`](/rich-text-editor/api-inlineModeModel.html) option of inlineMode makes the inline Rich Text Editor to appear.  You can select the text in the editable area otherwise the inline Rich Text Editor will be appear once click into the editable area.

{% tab template="rich-text-editor/getting-started", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript

/**
* RTE Inline mode Sample
*/
import { Component } from '@angular/core';
import { ToolbarService, LinkService, ImageService, HtmlEditorService, QuickToolbarService } from '@syncfusion/ej2-angular-richtexteditor';
@Component({
selector: 'app-root',
template: `<ejs-richtexteditor id='inlineRTE' #inlineRTE [inlineMode]='inlineMode' [toolbarSettings]='toolbarSettings' [format]='format' [fontFamily]='fontFamily'>
            <ng-template #valueTemplate>
                <p>The sample is configured with inline mode of editor. Initially, the editor is rendered without a <a href="https://ej2.syncfusion.com/home/" target="_blank">toolbar</a>. The toolbar becomes visible only when the content is selected.</p>
            </ng-template>
          </ejs-richtexteditor>`,
providers: [ToolbarService, LinkService, ImageService, HtmlEditorService, QuickToolbarService]
})
export class AppComponent  {
public inlineMode: object = { enable: true, onSelection: true };
public toolbarSettings: Object = {
    items: ['Bold', 'Italic', 'Underline',
        'Formats', '-', 'Alignments', 'OrderedList', 'UnorderedList',
        'CreateLink']
};
public format: Object = {
    width: 'auto'
};
public fontFamily: Object = {
    width: 'auto'
};
}

```

{% endtab %}