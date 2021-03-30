# Table

RichTextEditor allows to insert table of content in edit panel and provides an options to add, edit and remove the table as well as perform other table related action. For inserting the table to the Rich Text Editor, the following list of options have been provided in the [`tableSettings`](../api/rich-text-editor/tableSettingsModel/)

| Options | Description | Default Value |
|----------------|---------|-----------------------------|
| minWidth | Sets the default minWidth of the table. | 0 |
| maxWidth | Sets the default maxWidth of the table. | null |
| resize | Enable resize feature in table.| true |
| styles | This is an array of key value pair, on each pair, key should be name of styling and value is class name. this list will be shown on quick toolbar options to change the styles of table on designing like dashed, double bordered. | [`TableStyleItems`](../api/rich-text-editor/tableSettingsModel/#styles) |
| width | Sets the default width of the table. | 100% |

> To use Table feature, inject `TableService` in the provider section of `AppModule`.

## Insert table

Using the `table` toolbar option, select a number of rows and columns to be inserted over the table
grid and insert table into Rich Text Editor content using the mouse.

Tables can also be inserted through the `Insert Table` option in the pop-up where the number of rows
and columns can be provided manually,and this is the default way in devices.

In the following sample, the table has been injected from table module.

{% tab template="rich-text-editor/getting-started", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript

    import { Component } from '@angular/core';
import { ToolbarService, LinkService, ImageService, HtmlEditorService, TableService } from '@syncfusion/ej2-angular-richtexteditor';
@Component({
selector: 'app-root',
template: `<ejs-richtexteditor id='iframeRTE' [toolbarSettings]='tools'>
              <ng-template #valueTemplate>
                <p>The Rich Text Editor component is WYSIWYG ("what you see is what you get") editor
                that provides the best user experience to create and update the content.
                Users can format their content using standard toolbar commands.</p>

                <p><b>Key features:</b></p>

                <ul><li><p>Provides &lt;IFRAME&gt; and &lt;DIV&gt; modes</p></li>
                <li><p>Capable of handling markdown editing.</p></li>
                <li><p>Contains a modular library to load the necessary functionality on demand.</p></li>
                <li><p>Provides a fully customizable toolbar.</p></li>
                <li><p>Provides HTML view to edit the source directly for developers.</p></li>
                <li><p>Supports third-party library integration.</p></li>
                <li><p>Allows preview of modified content before saving it.</p></li>
                <li><p>Handles images, hyperlinks, video, hyperlinks, uploads, etc.</p></li>
                <li><p>Contains undo/redo manager.</p></li>
                <li><p>Creates bulleted and numbered lists.</p></li>
                </ul>
              </ng-template>
            </ejs-richtexteditor>`,
providers: [ToolbarService, LinkService, ImageService, HtmlEditorService, TableService]
})
export class AppComponent  {
    public tools: object = {
        items: ['CreateTable']
    };
}

```

{% endtab %}

## Quick Toolbar

Quick toolbar will open by clicking on the table. It has different sets of commands to be performed on
the table which increases the feasibility to edit the table easily.

## Table Header

`Table Header` command is available with quick toolbar option through which the header row can be
added or removed from the inserted table. The following image illustrates the table header.

![RTE table header](images/table_header.png)

## Insert Rows

`Rows` can be inserted above or below the required table cell through the quick toolbar. Also,
focused row can be deleted. The following screenshot shows the available options of the row item.

![RTE table row](images/table_rows.png)

## Insert Columns

`Columns` can be inserted to the left or right side of the required table cell through the quick
toolbar. Also, the focused column can be deleted. The following screenshot shows the available
options in inserting column item.

![RTE table column](images/table_column.png)

## Set Color

The background color can be set for each table cell through the `background color` command available
in quick toolbar.

![RTE table background color](images/table_bg_color.png)

## Delete Table

Using the delete item in the quick toolbar, users can delete the entire table.

## Vertical Align

Text inside the table can be aligned to top, middle, or bottom using the `tableCellVerticalAlign`
tool of the quick toolbar.

![RTE table vertical alignment](images/table_vertical.png)

## Horizontal Align

Text inside the table can be aligned left, right, or center using the `tableCellHorizontalAlign` tool
of the quick toolbar.

![RTE table horizontal alignment](images/table_horizontal.png)

## Table Styles

Table styles provided for class name should be appended to a table element. It helps to design the
table in specific CSS styles when inserting in the editor.

By Default, provides Dashed border and Alternate rows.

**Dashed border**: Applies the dashed border to the table.

**Alternate border**: Applies the alternative background to the table.

![RTE table styles](images/table_style.png)

## Table Properties

Sets the default width of the table when it is inserted in the Rich Text Editor using the width of
`tableSettings`.

Using the quick toolbar, users can change the width, cell padding, and cell spacing in the selected
table using the properties option.

![RTE table settings](images/table_properties.png)

## Table cell merge and split

The Rich Text Editor allows users to change the appearance of the tables by splitting or merging the table cells.

`TableCell` item should be configured in the Table [quickToolbarSettings](../api/rich-text-editor/quickToolbarSettings/#table) Property to show the merge/split icons while selecting the table cells

### Table cell merge

The table cell merge feature allows you to merge two or more row and column cells into a single cell with its contents.

The following image explains the table merge action.

![RTE table cell merge](./images/table_merge.png)

### Table cell split

The table cell split feature allows you to a selected cell can be split both horizontally and vertically.

The following image explains the table split action.

![RTE table cell split](./images/table_split.png)