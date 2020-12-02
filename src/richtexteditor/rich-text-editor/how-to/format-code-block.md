---
title: "Rich Text Editor how to format code block using toolbar button"
component: "Rich Text Editor"
description: "This section for Syncfusion Angular Rich Text Editor component explains about how to format code block using toolbar button."
---

# Format code block using toolbar button

You can configure code block formatting as a separate toolbar button by adding the **InsertCode** keyword within the [`toolbarSettings`](./../../api/rich-text-editor/toolbarSettings/#toolbarsettings) items property.

The InsertCode button has a toggle state to apply code block formatting to the editor and remove code block formatting from the editor.

The following sample demonstrates how to config the InsertCode button in toolbar and set the background color to “pre” tag for highlighting the code block.

{% tab template="rich-text-editor/how-to/format-code-block", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { ToolbarService, LinkService, ImageService, HtmlEditorService  } from '@syncfusion/ej2-angular-richtexteditor';
@Component({
  selector: 'app-root',
  template: `<ejs-richtexteditor id='defaultRTE' #sample [toolbarSettings]='tools'>
  <ng-template #valueTemplate>
    <p>The Rich Text Editor triggers events based on its actions. </p>
    <p> The events can be used as an extension point to perform custom operations.</p>
    <ul>
      <li>created - Triggers when the component is rendered.</li>
      <li>change - Triggers only when RTE is blurred and changes are done to the content.</li>
      <li>focus - Triggers when RTE is focused in.</li>
      <li>blur - Triggers when RTE is focused out.</li>
      <li>actionBegin - Triggers before command execution using toolbar items or executeCommand method.</li>
      <li>actionComplete - Triggers after command execution using toolbar items or executeCommand method.</li>
      <li>destroyed – Triggers when the component is destroyed.</li>
    </ul>
    </ng-template>
  </ejs-richtexteditor>`,
  providers: [ToolbarService, LinkService, ImageService, HtmlEditorService ]
})
export class AppComponent  {
   public tools: object = {
      items: ['InsertCode']
  };
}

```

{% endtab %}
