---
title: "Angular Rich Text Editor Toolbar configuration"
component: "Rich Text Editor"
description: "This section for Syncfusion's Angular Rich Text Editor component explains the toolbar which provides a set of commands for editing and formatting the content."
---

# Toolbar

The Rich Text Editor toolbar contains a collection of tools such as bold, italic and text alignment buttons that are used to format the content. However, in most integrations, you can customize the toolbar configurations easily to suit your needs.

To use Toolbar feature, inject `ToolbarService` in the provider section of `AppModule`.

The Rich Text Editor allows you to configure different types of toolbar using [`type`](../api/rich-text-editor/toolbarSettings/#type) field in [`toolbarSettings`](../api/rich-text-editor/toolbarSettings/) property. The types of toolbar are:

1. Expand
2. MultiRow

## Expand Toolbar

The default mode of [`toolbar`](../api/rich-text-editor/toolbarSettings/#type) is Expand, it will hide the overflowing items in the next row. Click the expand arrow to view overflowing toolbar items.

{% tab template="rich-text-editor/toolbar/expand", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript
  import { Component } from '@angular/core';
import { ToolbarService, HtmlEditorService } from '@syncfusion/ej2-angular-richtexteditor';
@Component({
    selector: 'app-root',
    template: `<ejs-richtexteditor id='defaultRTE' [toolbarSettings]='tools'>
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
    providers: [ToolbarService, HtmlEditorService]
})
export class AppComponent  {
    public tools: object = {
        type: 'Expand',
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

## Multi-row Toolbar

Set the type as `MultiRow` in [`toolbarSettings`](../api/rich-text-editor/toolbarSettings/#type) to hide the overflowing items in the next row. All toolbar items are visible.

{% tab template="rich-text-editor/toolbar/multirow", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript

import { Component } from '@angular/core';
import { ToolbarService, HtmlEditorService } from '@syncfusion/ej2-angular-richtexteditor';
@Component({
    selector: 'app-root',
    template: `<ejs-richtexteditor id='defaultRTE' [toolbarSettings]='tools'>
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
    providers: [ToolbarService, HtmlEditorService]
})
export class AppComponent  {
    public tools: object = {
        type: 'MultiRow',
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

## Floating Toolbar

By default, the toolbar is floating at the top of the Rich Text Editor on scrolling. It can be customized by specifying the offset of the floating toolbar from document's top position using[`floatingToolbarOffset`](../api/rich-text-editor/#floatingtoolbaroffset).

Can Enable or disable the floating toolbar using [`enableFloating`](../api/rich-text-editor/toolbarSettings/#enablefloating) property.

{% tab template="rich-text-editor/floating-toolbar", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { ToolbarService, HtmlEditorService, QuickToolbarService, RichTextEditorComponent} from '@syncfusion/ej2-angular-richtexteditor';
import { CheckBoxComponent } from '@syncfusion/ej2-angular-buttons';
@Component({
    selector: 'app-root',
    template: `<ejs-richtexteditor #typeRTE id='defaultRTE' [toolbarSettings]='tools'>
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
    </ejs-richtexteditor>
     <div>
    <ejs-checkbox #float label="Enable Floating" [checked]="true" (change)="onChangeFloat()"></ejs-checkbox>
    </div>`,
    providers: [ToolbarService, HtmlEditorService, QuickToolbarService]
})
export class AppComponent  {
@ViewChild('float') rteFloatObj: CheckBoxComponent;
@ViewChild('typeRTE') rteObj: RichTextEditorComponent;
  public tools: object = {
      enableFloating: false
  };
  public onChangeFloat(): void {
      this.rteObj.toolbarSettings.enableFloating = this.rteFloatObj.checked;
      this.rteObj.dataBind();
  }
}

```

{% endtab %}

## Toolbar Items

The following table shows that list of available tools in the Rich Text Editor's toolbar.

| Name | Summary | Initialization |
|----------------|---------|------------------------------------------|
| Undo | Allows to Undo the previous actions.|toolbarSettings: { items: ['Undo']} |
| Redo | Allows to Redo the actions.|toolbarSettings: { items: ['Redo']}|
| Alignment | Align the content with left, center, and right margin.|toolbarSettings: { items: ['Alignments']}|
| OrderedList | Create a new list item(numbered). |toolbarSettings: { items: ['OrderedList']}|
| UnorderedList | Create a new list item(bulleted). |toolbarSettings: { items: ['UnorderedList']}|
| Indent | Allows to increase the indent level of the content.|toolbarSettings: { items: ['Indent']}|
| Outdent | Allows to decrease the indent level of the content.|toolbarSettings: { items: ['Outdent']}|
| Hyperlink | Creates a hyperlink to a text or image to a specific location in the content.|toolbarSettings: { items: ['CreateLink']}|
| Images | Inserts an image from an online source or local computer. |toolbarSettings: { items: ['Image']}|
| LowerCase | Change the case of selected text to lower in the content. |toolbarSettings: { items: ['LowerCase']}|
| UpperCase | Change the case of selected text to upper  in the content.|toolbarSettings: { items: ['UpperCase’']}|
| SubScript | Makes the selected text as subscript (lower).|toolbarSettings: { items: ['SubScript']}|
| SuperScript | Makes the selected text as superscript (higher).|toolbarSettings: { items: ['SuperScript’']}|
| Print | Allows to print the editor content. |toolbarSettings: { items: ['Print']}|
| FontName | Defines the fonts that appear under the Font Family DropDownList from the Rich Text Editor's toolbar. |toolbarSettings: { items: ['FontName']}|
| FontSize | Defines the font sizes that appear under the Font Size DropDownList from the Rich Text Editor's toolbar.|toolbarSettings: { items: ['FontSize']}|
| FontColor | Specifies an array of colors can be used in the colors popup for font color.|toolbarSettings: { items: ['FontColor']}|
| BackgroundColor | Specifies an array of colors can be used in the colors popup for background color.|toolbarSettings: { items: ['BackgroundColor']}|
| Format | An Object with the options that will appear in the Paragraph Format dropdown from the toolbar. |toolbarSettings: { items: ['Formats']}|
| StrikeThrough | Apply double line strike through formatting for the selected text. |toolbarSettings: { items: ['StrikeThrough']}|
| ClearFormat | The clear format tool is useful to remove all formatting styles (such as bold, italic, underline, color, superscript, subscript, and more) from currently selected text. As a result, all the text formatting will be cleared and return to its default formatting styles.|toolbarSettings: { items: ['ClearFormat']}|
| FullScreen | Stretches the editor to the maximum width and height of the browser window.|toolbarSettings: { items: ['FullScreen']}|
| SourceCode | Rich Text Editor includes the ability for users to directly edit HTML code via “Source View”. If you made any modification in Source view directly, synchronize with Design view.|toolbarSettings: { items: ['SourceCode']}|

By default, tool will be arranged in following order.

```typescript
items: ['Bold', 'Italic', 'Underline', '|', 'Formats', 'Alignments', 'OrderedList', 'UnorderedList','|', 'CreateLink', 'Image', '|', 'SourceCode', 'Undo', 'Redo']
```

The tools order can be customized as our application requirement. If you are not specifying any tools order, the editor will create the toolbar with default items.

## Custom tool

The Rich Text Editor allows you to configure your own commands to its toolbar using the  [`toolbarSettings`](../api/rich-text-editor/#toolbarSettings) property. The command can be plain text, icon, or HTML template. The order and the group can also be defined where the command should be included. Bind action to the command by getting its instance.

This sample shows how to add your own commands to the toolbar of the Rich Text Editor. The “Ω” command is added to insert special characters in the editor. By clicking the “Ω” command, it will show the special characters list, and then choose the character to be inserted in the editor.

The following code snippet illustrates custom tool with tooltip text which will be included in [`items`](../api/rich-text-editor/toolbarSettings/#items) field of the toolbarSettings property.

In the following sample the Dialog component will be created in Rich Text Editor's `created` event. And it's target is given to Rich Text Editor's content

```javascript

{
    tooltipText: 'Insert Symbol',
    undo: true,
    click: this.onClick.bind(this),
    template: '<button class="e-tbar-btn e-btn" tabindex="-1" id="custom_tbar" style="width:100%"><div class="e-tbar-btn-text" style="font-weight: 500;"> &#937;</div></button>'
}

```

{% tab template="rich-text-editor/getting-started", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { ToolbarService, LinkService, ImageService, HtmlEditorService, QuickToolbarService , RichTextEditorComponent, NodeSelection} from '@syncfusion/ej2-angular-richtexteditor';
import { Dialog } from '@syncfusion/ej2-popups';
@Component({
    selector: 'app-root',
    template: `<ejs-richtexteditor id='customRTE' #customRTE [toolbarSettings]='tools' (created)='onCreate()'>
            <ng-template #valueTemplate>
                <div style="display:block;"><p style="margin-right:10px">The custom
                command "insert special character" is configured as the last item of
                the toolbar.Click on the command and choose the special character you want
                to include from the popup.</p></div>
            </ng-template>
        </ejs-richtexteditor>
        <ejs-dialog #Dialog id="rteDialog" [buttons]='dlgButtons' (overlayClick)="dialogOverlay()" [header]='header' [visible]='false'
            [showCloseIcon]='false' [target]='target' (created)="dialogCreate()" [isModal]='true'>
            <ng-template #content>
                <div id="rteSpecial_char">
                    <div class="char_block" title="^">^</div>
                    <div class="char_block" title="_">_</div>
                    <div class="char_block" title="|">|</div>
                    <div class="char_block" title="¡">¡</div>
                    <div class="char_block" title="¢">¢</div>
                    <div class="char_block" title="£">£</div>
                    <div class="char_block" title="¤">¤</div>
                    <div class="char_block" title="¡">¡</div>
                    <div class="char_block" title="¢">¢</div>
                    <div class="char_block" title="£">£</div>
                    <div class="char_block" title="¤">¤</div>
                    <div class="char_block" title="¥">¥</div>
                    <div class="char_block" title="₹">₹</div>
                    <div class="char_block" title="¦">¦</div>
                    <div class="char_block" title="§">§</div>
                    <div class="char_block" title="¨">¨</div>
                    <div class="char_block" title="©">©</div>
                    <div class="char_block" title="ª">ª</div>
                    <div class="char_block" title="«">«</div>
                </div>
            </ng-template>
        </ejs-dialog>`,
    providers: [ToolbarService, LinkService, ImageService, HtmlEditorService, QuickToolbarService]
})
export class AppComponent  {
@ViewChild('customRTE')
public rteObj: RichTextEditorComponent;
@ViewChild('Dialog')
public dialogObj: Dialog;
public selection: NodeSelection = new NodeSelection();
public ranges: Range;
public tools: object = {
    items: ['Bold', 'Italic', 'Underline', '|', 'Formats', 'Alignments', 'OrderedList',
    'UnorderedList', '|', 'CreateLink', 'Image', '|', 'SourceCode',
    {
        tooltipText: 'Insert Symbol',
        undo: true,
        click: this.onClick.bind(this),
        template: '<button class="e-tbar-btn e-btn" tabindex="-1" id="custom_tbar"  style="width:100%">'
                  + '<div class="e-tbar-btn-text" style="font-weight: 500;"> Ω</div></button>'
    }, '|', 'Undo', 'Redo'
    ]
};
public dlgButtons: any = [{ buttonModel: { content: "Insert", isPrimary: true }, click: this.onInsert.bind(this) },
{ buttonModel: { content: 'Cancel' }, click: this.dialogOverlay.bind(this) }];
public header: string = 'Special Characters';
public target: HTMLElement = document.getElementById('rteSection');
public height: any = '350px';
public onCreate(): void {
    let customBtn: HTMLElement = document.getElementById('custom_tbar') as HTMLElement;
    this.dialogObj.target = document.getElementById('rteSection');
}
public dialogCreate(): void {
    let dialogCtn: HTMLElement = document.getElementById('rteSpecial_char');
    dialogCtn.onclick = (e: Event) => {
        let target: HTMLElement = e.target as HTMLElement;
        let activeEle: Element = this.dialogObj.element.querySelector('.char_block.e-active');
        if (target.classList.contains('char_block')) {
            target.classList.add('e-active');
            if (activeEle) {
                activeEle.classList.remove('e-active');
            }
        }
    };
}

public onClick() {
    this.rteObj.focusIn();
    this.ranges = this.selection.getRange(document);
    this.dialogObj.width = this.rteObj.element.offsetWidth * 0.5;
    this.dialogObj.dataBind();
    this.dialogObj.show();
    this.dialogObj.element.style.maxHeight = 'none';
}

public onInsert(): void {
    let activeEle: Element = this.dialogObj.element.querySelector('.char_block.e-active');
    if (activeEle) {
        this.ranges.insertNode(document.createTextNode(activeEle.textContent));
    }
    this.dialogOverlay();
}

public dialogOverlay(): void {
    let activeEle: Element = this.dialogObj.element.querySelector('.char_block.e-active');
    if (activeEle) {
        activeEle.classList.remove('e-active');
    }
    this.dialogObj.hide();
}
}

```

{% endtab %}

## Quick inline toolbar

Quick commands are opened as context-menu on clicking the corresponding element. The commands must be passed as string collection to image, text, and link attributes of the [`quickToolbarSettings`](../api/rich-text-editor/#quickToolbarSettings) property.

| Target Element | Default Quick Toolbar items |
|----------------|---------|
|image | 'Replace', 'Align', 'Caption', 'Remove', 'InsertLink', 'Display', 'AltText','Dimension'.|
| link | 'Open', 'Edit', 'UnLink'.|
| text | 'Cut', 'Copy', 'Paste'.|
| table| 'tableHeader', 'tableRows', 'tableColumns', 'backgroundColor', '-', 'tableRemove', 'alignments', 'tableCellVerticalAlign', 'styles'.|

Custom tool can be added to the corresponding quick toolbar, using [`quickToolbarSettings`](../api/rich-text-editor/#quickToolbarSettings) property.

The following sample demonstrates the option to insert the image to the Rich Text Editor content as well as option to rotate the image through the quick toolbar. The image rotation functionalities have been achieved through the `toolbarClick` event.

{% tab template="rich-text-editor/quick-toolbar", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { ToolbarService, LinkService, ImageService, HtmlEditorService,
QuickToolbarService, RichTextEditorComponent, QuickToolbarSettingsModel } from '@syncfusion/ej2-angular-richtexteditor';
@Component({
    selector: 'app-root',
    template: `<ejs-richtexteditor #imageRTE id='imageRTE' [(quickToolbarSettings)]='quickToolbarSettings'>
            <ng-template #valueTemplate>
                <p>RichTextEditor allows to insert images from online source as well as local
                    computer where you want to insert the image in your content.</p>
                <p><b>Get started Quick Toolbar to click on the image</b></p>
                <p>It is possible to add custom style on the selected image inside the Rich Text Editor through quick toolbar.</p>
                <img id="rteImageID" style="width:300px; height:300px;transform: rotate(0deg);" alt="Logo" src="http://ej2.syncfusion.com/angular/demos/src/rte/images/RTEImage-Feather.png">
            </ng-template>
        </ejs-richtexteditor>`,
    providers: [ToolbarService, LinkService, ImageService, HtmlEditorService, QuickToolbarService]
})
export class AppComponent  {
    @ViewChild('imageRTE') rteObj: RichTextEditorComponent;
    quickToolbarSettings: QuickToolbarSettingsModel = {
        image: [
            'Replace', 'Align', 'Caption', 'Remove', 'InsertLink', 'OpenImageLink', '-',
            'EditImageLink', 'RemoveImageLink', 'Display', 'AltText', 'Dimension'
        ]
    };
}

```

{% endtab %}

> To use quick toolbar feature, inject `QuickToolbarService, ImageService, LinkService` in the provider section of `AppModule`.