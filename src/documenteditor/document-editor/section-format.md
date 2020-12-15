---
title: "Working with Section Formatting"
component: "DocumentEditor"
description: "Learn section formatting supported in JavaScript document editor like page size and margins, and how to customize it."
---

# Working with Section Formatting

Document editor supports various section formatting such as page size, page margins, and more.

## Page size

You can get or set the size of a section at cursor position by using the following sample code.

```typescript
this.documentEditor.selection.sectionFormat.pageWidth = 500;
this.documentEditor.selection.sectionFormat.pageHeight = 600;
```

You can change the orientation of the page by swapping the values of page width and height respectively.

## Page margins

Left and right page margin defines the gap between the document content from left and right side of the page respectively. Top and bottom page margins defines the gap between the document content from header and footer of the page respectively.
Refer to the following sample code.

```typescript
this.documentEditor.selection.sectionFormat.leftMargin = 10;
this.documentEditor.selection.sectionFormat.rightMargin = 10;
this.documentEditor.selection.sectionFormat.bottomMargin = 10;
this.documentEditor.selection.sectionFormat.topMargin = 10;
```

## Header distance

You can define the distance of header content from the top of the page by using the following sample code.

```typescript
this.documentEditor.selection.sectionFormat.headerDistance = 72;
```

## Footer distance

You can define the distance of footer content from the bottom of the page by using the following sample code.

```typescript
this.documentEditor.selection.sectionFormat.footerDistance = 72;
```

## See Also

*[Page setup dialog](../document-editor/dialog#page-setup-dialog/)