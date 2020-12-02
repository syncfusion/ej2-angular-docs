---
title: "Angular Rich Text Editor Iframe mode"
component: "Rich Text Editor"
description: "This section for Syncfusion's Angular Rich Text Editor component demonstrates the default rendering of the Rich Text Editor in iframe mode."
---

# Iframe

When the [iframeSettings](../api/rich-text-editor/#iframesettings) option is enabled, the Rich Text Editor creates the iframe element as the content area on control initialization. It is used to display and editing the content in content area. The editor will display only the body tag of a < iframe > document.

{% tab template="rich-text-editor/getting-started", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript

    /**
     * RTE IFrame Sample
     */
    import { Component } from '@angular/core';
    import { ToolbarService, LinkService, ImageService, HtmlEditorService } from '@syncfusion/ej2-angular-richtexteditor';
    @Component({
        selector: 'app-root',
        template: `<ejs-richtexteditor id='iframeRTE' [iframeSettings]='iframe'></ejs-richtexteditor>`,
        providers: [ToolbarService, LinkService, ImageService, HtmlEditorService]
    })
    export class AppComponent  {
        public iframe: object = { enable: true };
    }

```

{% endtab %}

## IFrame attributes

The editor allows you to pass an additional attribute to body tag of a < iframe > element using attributes fields of the [`iframeSettings`](../api/rich-text-editor/#iframesettings) property. This property contains name/value pairs in string format. It is used to override the default appearance of the content area.

{% tab template="rich-text-editor/getting-started", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript

    /**
     * RTE IFrame attributes Sample
     */

import { Component } from '@angular/core';
import { ToolbarService, LinkService, ImageService, HtmlEditorService } from '@syncfusion/ej2-angular-richtexteditor';
@Component({
    selector: 'app-root',
    template: `<ejs-richtexteditor id='iframeRTE' [iframeSettings]='iframe'></ejs-richtexteditor>`,
    providers: [ToolbarService, LinkService, ImageService, HtmlEditorService]
})
export class AppComponent  {
    public iframe: object = {
        enable: true,
        attributes: {
            readonly: 'readonly'
        }
    };
}

```

{% endtab %}

## Adding external CSS/Script file

The editor offers you to add external CSS file to style the < iframe > element. Easily change the appearance of editor’s content using an external CSS file using [`styles`](../api/rich-text-editor/#iframesettings) field in the iframeSettings property.

Likewise, add the external script file to the `< iframe >` element using the [`scripts`](../api/rich-text-editor/#iframesettings) field of iframeSettings to provide the additional functionalities to the RichTextEditor.

{% tab template="rich-text-editor/getting-started", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript

    /**
     * RTE IFrame Sample
     */
    import { Component } from '@angular/core';
    import { ToolbarService, LinkService, ImageService, HtmlEditorService } from '@syncfusion/ej2-angular-richtexteditor';
    @Component({
    selector: 'app-root',
    template: `<ejs-richtexteditor id='iframeRTE' [iframeSettings]='iframe'></ejs-richtexteditor>`,
    providers: [ToolbarService, LinkService, ImageService, HtmlEditorService]
    })
    export class AppComponent  {
        public iframe: object = {
            enable: true,
            attributes: {
                readonly: 'readonly'
            },
            resources: {
                scripts: [''],  // script.js
                styles: ['']    // css
            }
        };
    }
```

{% endtab %}