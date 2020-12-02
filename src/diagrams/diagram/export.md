---
title: "Export"
component: "Diagram"
description: "Diagram exporting supports to export the diagram content as image/svg."
---

# Exporting

Diagram provides support to export its content as image/svg files.
The client-side method [`exportDiagram`](../api/diagram#exportDiagram) helps to export the diagram. The following code illustrates how to export the diagram as image.
>Note: To use Print and Export, you need to inject `PrintAndExport` in the diagram.

<!-- markdownlint-disable MD033 -->

```typescript
public options: IExportOptions;
this.options  = {};
this.options.mode = 'Data';
this.diagram.exportDiagram(this.options);
```

## Exporting options

Diagram provides support to export the desired region of the diagram to desired formats.

## File Name

[`FileName`](../api/diagram/iExportOptions#fileName-string) is the name of the file to be downloaded. By default, the file name is set to **Diagram**.

## Format

[`Format`](../api/diagram/iExportOptions#format-fileformat) is to specify the type/format of the exported file. By default, the diagram is exported as .jpg format. You can export diagram to the following formats:

* JPG
* PNG
* BMP
* SVG

```typescript
public options: IExportOptions;
this.options = {};
this.options.mode = 'Data';
this.options.format = 'SVG';
this.diagram.exportDiagram(this.options);
```

## Margin

[`Margin`](../api/diagram/iExportOptions#margin-marginmodel) specifies the amount of space that has to be left around the diagram.

<!-- markdownlint-disable MD033 -->

```typescript
public options: IExportOptions;
this.options = {};
this.options.mode = 'Data';
this.options.margin = { left: 10, right: 10, top: 10, bottom: 10};
this.options.fileName = 'format';
this.options.format = 'SVG';
this.diagram.exportDiagram(this.options);

```

## Mode

[`Mode`](../api/diagram/iExportOptions#mode-exportmodes) specifies whether the diagram is to be exported as files or as data (ImageURL/SVG). The exporting options are as follows:

* Data: Exports and downloads the diagram as image.
* Download: Exports the diagram as data of formats ImageURL/SVG.

For more information about the exporting modes, refer to Exporting Modes.

The following code example illustrates how to export the diagram as raw data.

```typescript
public options: IExportOptions;
this.options = {};
this.options.mode = 'Data';
this.options.margin = { left: 10, right: 10, top: 10, bottom: 10};
this.options.fileName = 'format';
this.options.format = 'SVG';
this.diagram.exportDiagram(this.options);

```

## Region

You can export any particular [`region`](../api/diagram/iExportOptions#region-diagramregions) of the diagram and the region is categorized as follows.

* Region that fits all nodes and connectors that are added to model.
* Region that fits all pages (single or multiple pages based on page settings).

For more information about region, refer to Regions.

The following code example illustrates how to export the region occupied by the diagram elements.

```typescript
public options: IExportOptions;
this.options = {};
this.options.mode = 'Data';
this.options.margin = { left: 10, right: 10, top: 10, bottom: 10};
this.options.fileName = 'format';
this.options.format = 'SVG';
this.options.region = 'Content';
this.diagram.exportDiagram(this.options);

```

## Custom bounds

Diagram provides support to export any specific region of the diagram by using [`bounds`](../api/diagram/iExportOptions#bounds-rect).

The following code example illustrates how to export the region occupied by the diagram elements.

```typescript
public options: IExportOptions;
this.options = {};
this.options.mode = 'Data';
this.options.margin = { left: 10, right: 10, top: 10, bottom: 10};
this.options.fileName = 'region';
this.options.format = 'SVG';
this.options.region = 'CustomBounds';
this.options.bounds.x = 10;
this.options.bounds.y = 10;
this.options.bounds.height = 100;
this.options.bounds.width = 100;
this.diagram.exportDiagram(this.options);
```

## Export diagram with stretch option

Diagram provides support to export the diagram as image for [`stretch`](../api/diagram/iExportOptions#stretch-stretch) option. The exported images will be clearer but larger in file size.

The following code example illustrates how to export the region occupied by the diagram elements.

```typescript
public options: IExportOptions;
this.options = {};
this.options.mode = 'Data';
this.options.margin = { left: 10, right: 10, top: 10, bottom: 10};
this.options.fileName = 'region';
this.options.format = 'SVG';
this.options.region = 'Content';
this.options.stretch = 'Stretch';
this.diagram.exportDiagram(this.options);
```

## Print

The client-side method [`print`](../api/diagram#print) helps to print the diagram as image.

| Name | Type | Description|
|-------- | -------- | -------- |
| region | enum | Sets the region of the diagram to be printed. |
| bounds | object | Prints any custom region of diagram. |
| stretch| enum | Resizes the diagram content to fill its allocated space and printed.|
| multiplePage | boolean | Prints the diagram into multiple pages. |
| pageWidth | number | Sets the page width of the diagram while printing the diagram into multiple pages. |
| pageHeight| number | Sets the page height of the diagram while printing the diagram into multiple pages.|
| pageOrientation | enum | Sets the orientation of the page. |

The following code example illustrates how to export the region occupied by the diagram elements.

```typescript
public options: IExportOptions;
this.options = {};
this.options.mode = 'Data';
this.options.region = 'PageSettings';
this.options.multiplePage = true;
this.options.pageHeight = 300;
this.options.pageWidth = 300;
this.diagram.print(this.options);
```
