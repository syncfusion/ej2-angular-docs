---
title: "Rich Text Editor How To customize the shorcut key"
component: "Rich Text Editor"
description: "This section for Syncfusion Angular Rich Text Editor component explains on how to customize the shortcut keys."
---

# Customize shortcut keys

It can be achieved by using [`formatter`](../../api/rich-text-editor/#formatter) property. You need to create `customformatterModel` to configure the `keyConfig` using `IHtmlFormatterModel` class and assign the same to the formatter property. Here, `ctrl+q` is configured to open the `Insert Hyperlink` dialog.

{% tab template="rich-text-editor/how-to/cut-copy", sourceFiles="app/**/*.ts,index.html" %}

```typescript

import { Component } from '@angular/core';
import { ToolbarService, LinkService, ImageService } from '@syncfusion/ej2-angular-richtexteditor';
import { HtmlEditorService, IHtmlFormatterModel, HTMLFormatter } from '@syncfusion/ej2-angular-richtexteditor';

@Component({
selector: 'app-root',
template: `<ejs-richtexteditor id='defaultRTE' #sample [formatter]='formatter'>
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
public customHTMLModel: IHtmlFormatterModel = { // formatter is used to configure the custom key
keyConfig: {
'insert-link': 'ctrl+q', // confite the desired key
}
};
public formatter: any = new HTMLFormatter(this.customHTMLModel); // to configure custom key

}

```

{% endtab %}

> You need to import `IHtmlFormatterModel` and `HTMLFormatter` to configure the shortcut key.
