---
title: "Module Injection"
component: "Grid"
description: "Learn what are the feature modules are available in EJ2 Grid."
---

# Feature Modules

The following value providers should be injected to extend grid's functionality.

| Module | Description |
|------|-------------|
| [`PageService`](../api/grid/page)| Inject this module to use paging feature.|
| [`SortService`](../api/grid/sort)| Inject this module to use sorting feature.|
| [`FilterService`](../api/grid/filter)| Inject this module to use filtering feature.|
| [`GroupService`](../api/grid/group)| Inject this module to use grouping feature|
| [`EditService`](../api/grid/edit)| Inject this module is use editing feature.|
| `AggregateService`| Inject this module to use aggregate feature.|
| [`ColumnChooserService`](../api/grid/columnChooser)| Inject this module to use column chooser feature.|
| `ColumnMenuService`| Inject this module to use column menu feature.|
| `CommandColumnService`| Inject this module to use command column feature.|
| [`ContextMenuService`](../api/grid/contextMenu)| Inject this module to use context menu feature.|
| [`DetailRowService`](../api/grid/detailRow)| Inject this module to use detail template feature.|
| `ForeignKeyService`| Inject this module to use foreign key feature.|
| `FreezeService`| Inject this module to use frozen rows and columns feature.|
| `ResizeService`| Inject this module to use resize feature.|
| [`ReorderService`](../api/grid/reorder)| Inject this module to use reorder feature.|
| `RowDDService`| Inject this module to use row drag and drop feature.|
| [`SearchService`](../api/grid/search)| Inject this module to use search feature and this is a default injected module.|
| [`SelectionService`](../api/grid/selection)| Inject this module to use selection feature and this is a default injected module.|
| [`ScrollService`](../api/grid/scroll)| Inject this module to use scrolling feature and this is a default injected module.|
| [`PrintService`](../api/grid/print)| Inject this module to use to use print feature and this is a default injected module.|
| `ToolbarService`| Inject this module to use toolbar feature.|
| `VirtualScrollService`| Inject this module to use virtual scroll feature.|
| `ExcelExportService`| Inject this module to use excel export feature.|
| `PdfExportService`| Inject this module to use PDF export feature.|

These modules should be injected into the **providers** section of root **NgModule** or component class.
