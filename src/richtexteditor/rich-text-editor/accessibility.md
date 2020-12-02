---
title: "Rich Text Editor Accessibility"
component: "Rich Text Editor"
description: "This section explains the WAI-ARIA accessibility support of Syncfusion Angular Rich Text Editor component."
---

# Accessibility

The Rich Text Editor component has been designed, keeping in mind the WAI-ARIA specifications and applies the WAI-ARIA roles, states and properties. This component is characterized by complete ARIA accessibility support that makes it easy for people who use assistive technologies (AT) or those who completely rely on keyboard navigation.

## ARIA attributes

* The toolbar of Rich Text Editor, assigned the role of ‘Toolbar’ and has the following list of aria attribute.

| **Property** | **Functionalities** |
| --- | --- |
| role="toolbar" | This attribute added to the ToolBar element describes the actual role of the element. |
| aria-orientation     | Indicates the ToolBar orientation. Default value is `horizontal`. |
| aria-haspopup       | Indicates the popup mode of the Toolbar. Default value is false. When popup mode is enabled,  attribute value has to be changed to `true`. | |
| aria-disabled       | Indicates the disabled state of the ToolBar. |

For further details of Toolbar ARIA attributes, please look in to [`Accessibility of Toolbar`](../../toolbar/accessibility.html) documentation.

* The Rich Text Editor element is assigned the role of `application`.

| **Property** | **Functionalities** |
| --- | --- |
| role="application" | This attribute added to the Rich Text Editor element describes the actual role of the element. |
| aria-disabled       | Indicates the disabled state of the ToolBar. |

{% tab template="rich-text-editor/getting-started", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript
    import { Component } from '@angular/core';
    import { ToolbarService, LinkService, ImageService, HtmlEditorService} from '@syncfusion/ej2-angular-richtexteditor';
    @Component({
    selector: 'app-root',
    template:`<ejs-richtexteditor #defaultRTE id='defaultRTE' [toolbarSettings]='tools'></ejs-richtexteditor>`,
    providers: [ToolbarService, LinkService, ImageService, HtmlEditorService]
    })
    export class AppComponent  {
        public tools = {
            items: ['Bold', 'Italic', 'Underline', 'StrikeThrough',
        'FontName', 'FontSize', 'FontColor', 'BackgroundColor',
        'LowerCase', 'UpperCase', '|',
        'Formats', 'Alignments', 'OrderedList', 'UnorderedList',
        'Outdent', 'Indent', '|',
        'CreateLink', 'Image', '|', 'ClearFormat', 'Print',
        'SourceCode', 'FullScreen', '|', 'Undo', 'Redo']
        };
    }

```

{% endtab %}