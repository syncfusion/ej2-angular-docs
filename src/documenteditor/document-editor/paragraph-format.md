---
title: "Working with Paragraph Formatting"
component: "DocumentEditor"
description: "Learn paragraph formatting supported in JavaScript document editor and how to apply it for selected contents."
---

# Working with Paragraph Formatting

Document editor supports various paragraph formatting options such as text alignment, indentation, paragraph spacing, and more.

## Indentation

You can modify the left or right indentation of selected paragraphs using the following sample code.

```typescript
this.documentEditor.selection.paragraphFormat.leftIndent= 24;
this.documentEditor.selection.paragraphFormat.rightIndent= 24;
```

## Special indentation

You can define special indent for first line of the paragraph using the following sample code.

```typescript
this.documentEditor.selection.paragraphFormat.firstLineIndent= 24;
```

## Increase indent

You can increase the left indent of selected paragraphs by a factor of 36 points using the following sample code.

```typescript
this.documentEditor.editor.increaseIndent()
```

## Decrease indent

You can decrease the left indent of selected paragraphs by a factor of 36 points using the following sample code.

```typescript
this.documentEditor.editor.decreaseIndent()
```

## Text alignment

You can get or set the text alignment of selected paragraphs using the following sample code.

```typescript
this.documentEditor.selection.paragraphFormat.textAlignment= 'Center' | 'Left' | 'Right' | 'Justify';
```

You can toggle the text alignment of selected paragraphs by specifying a value using the following sample code.

```typescript
this.documentEditor.editor.toggleTextAlignment('Center' | 'Left' | 'Right' | 'Justify');
```

## Line spacing and its type

You can define the line spacing and its type for selected paragraphs using the following sample code.

```typescript
this.documentEditor.selection.paragraphFormat.lineSpacingType='AtLeast';
this.documentEditor.selection.paragraphFormat.lineSpacing= 6;
```

## Paragraph spacing

You can define the spacing before or after the paragraph by using the following sample code.

```typescript
this.documentEditor.selection.paragraphFormat.beforeSpacing= 24;
this.documentEditor.selection.paragraphFormat.afterSpacing= 24;
```

## Toolbar with paragraph formatting options

The following sample demonstrates the paragraph formatting options using a toolbar.

{% tab template="document-editor/paragraph-formatting",isDefaultActive=false, sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import {
    DocumentEditorComponent, EditorService, SelectionService, EditorHistoryService , SfdtExportService, ContextMenuService
} from '@syncfusion/ej2-angular-documenteditor';

@Component({
    selector: 'app-container',
    styleUrls: ['styles.css'],
    template: `<div style="width:100%;height:330px">
    <div>
        <ejs-toolbar (clicked)='toolbarButtonClick($event)'>
            <e-items>
                <e-item prefixIcon='e-de-icon-AlignLeft' id='AlignLeft' tooltipText='Align Left'></e-item>
                <e-item prefixIcon='e-de-icon-AlignCenter' id='AlignCenter' tooltipText='AlignCenter'></e-item>
                <e-item prefixIcon='e-de-icon-AlignRight' id='AlignRight' tooltipText='AlignRight'></e-item>
                <e-item prefixIcon='e-de-icon-Justify' id='Justify' tooltipText='Justify'></e-item>
                <e-item prefixIcon='e-de-icon-IncreaseIndent' id='IncreaseIndent' tooltipText='Increase Indent'></e-item>
                <e-item prefixIcon='e-de-icon-DecreaseIndent' id='DecreaseIndent' tooltipText='Decrease Indent'></e-item>
                <e-item type='Separator'></e-item>
                <e-item prefixIcon='e-de-icon-ClearAll' id='ClearFormat' tooltipText='ClearFormatting'></e-item>
            </e-items>
        </ejs-toolbar>
      </div>
  <ejs-documenteditor #document_editor (selectionChange)='onSelectionChange()' [enableSelection]='true' [isReadOnly]='false' [enableEditor]=true [enableEditorHistory]=true [enableSfdtExport]=true [enableContextMenu]=true style="display:block;width: 100%;height: 100%;"></ejs-documenteditor>
    </div>`,
    encapsulation: ViewEncapsulation.None,
    providers:[EditorService, SelectionService, EditorHistoryService , SfdtExportService, ContextMenuService]
})

export class AppComponent {
 @ViewChild('document_editor')
 public documentEditor: DocumentEditorComponent;

public toolbarButtonClick(arg: any) {
    switch (arg.item.id) {
        case 'AlignLeft':
            //Toggle the Left alignment for selected or current paragraph
            this.documentEditor.editor.toggleTextAlignment('Left');
            break;
        case 'AlignRight':
            //Toggle the Right alignment for selected or current paragraph
            this.documentEditor.editor.toggleTextAlignment('Right');
            break;
        case 'AlignCenter':
            //Toggle the Center alignment for selected or current paragraph
            this.documentEditor.editor.toggleTextAlignment('Center');
            break;
        case 'Justify':
            //Toggle the Justify alignment for selected or current paragraph
            this.documentEditor.editor.toggleTextAlignment('Justify');
            break;
        case 'IncreaseIndent':
            //Increase the left indent of selected or current paragraph
            this.documentEditor.editor.increaseIndent();
            break;
        case 'DecreaseIndent':
            //Decrease the left indent of selected or current paragraph
            this.documentEditor.editor.decreaseIndent();
            break;
        case 'ClearFormat':
            this.documentEditor.editor.clearFormatting();
            break;
    }
}

// Selection change to retrieve formatting
public onSelectionChange() {
    if (this.documentEditor.selection) {
        var paragraphFormat = this.documentEditor.selection.paragraphFormat;
        var toggleBtnId = ['AlignLeft', 'AlignCenter', 'AlignRight', 'Justify'];
        for (var i = 0; i < toggleBtnId.length; i++) {
            let toggleBtn: HTMLElement = document.getElementById(toggleBtnId[i]);
            toggleBtn.classList.remove('e-btn-toggle');
        }
        if (paragraphFormat.textAlignment === 'Left') {
            document.getElementById('AlignLeft').classList.add('e-btn-toggle');
        } else if (paragraphFormat.textAlignment === 'Right') {
            document.getElementById('AlignRight').classList.add('e-btn-toggle');
        } else if (paragraphFormat.textAlignment === 'Center') {
            document.getElementById('AlignCenter').classList.add('e-btn-toggle');
        } else {
            document.getElementById('Justify').classList.add('e-btn-toggle');
        }
        // #endregion
    }
}

}

```

{% endtab %}

## See Also

* [Feature modules](../document-editor/feature-module/)
* [Paragraph dialog](../document-editor/dialog#paragraph-dialog/)
* [Keyboard shortcuts](../document-editor/keyboard-shortcut#paragraph-formatting/)