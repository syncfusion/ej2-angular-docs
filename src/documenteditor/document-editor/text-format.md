---
title: "Working with Text Formatting"
component: "DocumentEditor"
description: "Learn text formatting supported in Angular document editor and how to apply it for selected contents."
---

# Working with Text Formatting

Document Editor supports several formatting options for text like bold, italic, font color, highlight color, and more. This section describes how to modify the formatting for selected text in detail.

## Bold

The bold formatting for selected text can be get or set by using the following sample code.

```typescript

//Gets the value for bold formatting of selected text.
let bold : boolean = documenteditor.selection.characterFormat.bold;
//Sets bold formatting for selected text.
documenteditor.selection.characterFormat.bold = true;

```

You can toggle the bold formatting based on existing value at selection. Refer to the following sample code.

```typescript
documenteditor.editor.toggleBold();
```

## Italic

The Italic formatting for selected text can be get or set by using the following sample code.

```typescript
documenteditor.selection.characterFormat.italic= true|false;
```

You can toggle the Italic formatting based on existing value at selection. Refer to the following sample code.

```typescript
documenteditor.editor.toggleItalic();
```

## Underline property

The underline style for selected text can be get or set by using the following sample code.

```typescript
documenteditor.selection.characterFormat.underline='Single' | 'None';
```

You can toggle the underline style of selected text based on existing value at selection by specifying a value. Refer to the following sample code.

```typescript
documenteditor.editor.toggleUnderline('Single');
```

## Strikethrough property

The strikethrough style for selected text can be get or set by using the following sample code.

```typescript
documenteditor.selection.characterFormat.strikethrough='Single' | 'Normal';
```

You can toggle the strikethrough style of selected text based on existing value at selection by specifying a value. Refer to the following sample code.

```typescript
documenteditor.editor.toggleStrikethrough();
```

## Superscript property

The selected text can be made superscript by using the following sample code.

```typescript
documenteditor.selection.characterFormat.baselineAlignment='Superscript';
```

Toggle the selected text as superscript or normal using the following sample code.

```typescript
documenteditor.editor.toggleSuperscript();
```

## Subscript property

The selected text can be made subscript by using the following sample code.

```typescript
documenteditor.selection.characterFormat.baselineAlignment='Subscript';
```

Toggle the selected text as subscript or normal using the following sample code.

```typescript
documenteditor.editor.toggleSubscript();
```

You can make a subscript or superscript text as normal using the following code.

```typescript
documenteditor.selection.characterFormat.baselineAlignment='Normal';
```

## Size

The size of selected text can be get or set using the following code.

```typescript
documenteditor.selection.characterFormat.fontSize= 32;
```

## Color

The color of selected text can be get or set using the following code.

```typescript
documenteditor.selection.characterFormat.fontColor= 'Pink';
documenteditor.selection.characterFormat.fontColor= '#FFC0CB';
```

## Font

The font style of selected text can be get or set using the following sample code.

```typescript
documenteditor.selection.characterFormat.fontFamily= 'Arial';
```

## Highlight color

The highlight color of the selected text can be get or set using the following sample code.

```typescript
documenteditor.selection.characterFormat.highlightColor= 'Pink';
documenteditor.selection.characterFormat.highlightColor= '#FFC0CB';
```

## Toolbar with options for text formatting

Refer to the following example.

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import {
    DocumentEditorComponent, EditorService, SelectionService, EditorHistoryService, SfdtExportService, ContextMenuService
} from '@syncfusion/ej2-angular-documenteditor';

@Component({
      selector: 'app-container',
      styleUrls: ['styles.css'],
      template: `<div>
      <div>
          <ejs-toolbar (clicked)='toolbarClickHandler($event)'>
              <e-items>
                  <e-item prefixIcon="e-de-ctnr-bold e-icons" tooltipText="Bold" id="bold"></e-item>
                  <e-item prefixIcon="e-de-ctnr-italic e-icons" tooltipText="Italic" id="italic"></e-item>
                  <e-item prefixIcon="e-de-ctnr-underline e-icons" tooltipText="Underline" id="underline"></e-item>
                  <e-item prefixIcon="e-de-ctnr-strikethrough e-icons" tooltipText="Strikethrough" id="strikethrough"></e-item>
                  <e-item prefixIcon="e-de-ctnr-subscript e-icons" tooltipText="Subscript" id="subscript"></e-item>
                  <e-item prefixIcon="e-de-ctnr-superscript e-icons" tooltipText="Superscript" id="superscript"></e-item>
                  <e-item type="Seperator"></e-item>
                  <e-item type="Input">
                  <ng-template #template>
                    <ejs-colorpicker [value]='#000000' [showButtons]=true (change)='onFontColorChange()' ></ejs-colorpicker>
                  </ng-template>
                  </e-item>
                  <e-item type="Seperator"></e-item>
                  <e-item type="Input">
                    <ng-template #template>
                        <ejs-combobox [dataSource]='fontStyle' [width]='120' [index]='2' [allowCustom]=true (change)='onFontFamilyChange()' [showClearButton]=false></ejs-combobox>
                    </ng-template>
                  </e-item>
                  <e-item type="Input">
                    <ng-template #template>
                      <ejs-combobox [dataSource]='fontSize' [width]='80' [index]='2' [allowCustom]='true' (change)='onFontSizeChange()'  [showClearButton]='false'></ejs-combobox>
                    </ng-template>
                  </e-item>
              </e-items>
          </ejs-toolbar>
        </div>
        <ejs-documenteditor #document_editor (selectionChange)='onSelectionChange()' [enableSelection]='true' [isReadOnly]='false' [enableEditor]=true [enableEditorHistory]=true [enableSfdtExport]=true [enableContextMenu]=true height="330px" style="display:block"></ejs-documenteditor>
      </div>`,
      encapsulation: ViewEncapsulation.None,
      providers: [EditorService, SelectionService, EditorHistoryService, SfdtExportService, ContextMenuService]
})
export class AppComponent {
    @ViewChild('document_editor')
    public documentEditor: DocumentEditorComponent;

    public fontStyle: string[] = ['Algerian', 'Arial', 'Calibri', 'Cambria', 'Cambria Math', 'Candara', 'Courier New', 'Georgia', 'Impact', 'Segoe Print', 'Segoe Script', 'Segoe UI', 'Symbol', 'Times New Roman', 'Verdana', 'Windings'];

    public fontSize: string[] = ['8', '9', '10', '11', '12', '14', '16', '18', '20', '22', '24', '26', '28', '36', '48', '72', '96'];

    public toolbarButtonClick(arg: any) {
        switch (arg.item.id) {
            case 'bold':
                //Toggles the bold of selected content
                this.documentEditor.editor.toggleBold();
                break;
            case 'italic':
                //Toggles the Italic of selected content
                this.documentEditor.editor.toggleItalic();
                break;
            case 'underline':
                //Toggles the underline of selected content
                this.documentEditor.editor.toggleUnderline('Single');
                break;
            case 'strikethrough':
                //Toggles the strikethrough of selected content
                this.documentEditor.editor.toggleStrikethrough();
                break;
            case 'subscript':
                //Toggles the subscript of selected content
                this.documentEditor.editor.toggleSubscript();
                break;
            case 'superscript':
                //Toggles the superscript of selected content
                this.documentEditor.editor.toggleSuperscript();
                break;
        }
    }
    public onFontFamilyChange(args) {
        this.documentEditor.ej2Instances.selection.characterFormat.fontFamily = args.value;
        this.documentEditor.focusIn();
    }
    public onFontSizeChange(args) {
        this.documentEditor.ej2Instances.selection.characterFormat.fontSize = args.value;
        this.documentEditor.focusIn();
    }
    public onFontColorChange(args) {
        this.documentEditor.ej2Instances.selection.characterFormat.fontColor = args.currentValue.hex;
        this.documentEditor.focusIn();
    }
    public onSelectionChange() {
        var characterformat = this.documentEditor.ej2Instances.selection.characterFormat;
        var properties = [characterformat.bold, characterformat.italic, characterformat.underline, characterformat.strikeThrough];
        var toggleBtnId = ["bold", "italic", "underline", "strikethrough"];
        for (var i = 0; i < properties.length; i++) {
            let toggleBtn: HTMLElement = document.getElementById(toggleBtnId[i]);
            if ((typeof (properties[i]) == 'boolean' && properties[i] == true) || (typeof (properties[i]) == 'string' && properties[i] !== 'None'))
                toggleBtn.classList.add("e-btn-toggle");
            else {
                if (toggleBtn.classList.contains("e-btn-toggle"))
                    toggleBtn.classList.remove("e-btn-toggle");
            }
        }
    }
}
```

## See Also

* [Feature modules](../document-editor/feature-module/)
* [Font dialog](../document-editor/dialog#font-dialog)
* [Keyboard shortcuts](../document-editor/keyboard-shortcut#text-formatting)