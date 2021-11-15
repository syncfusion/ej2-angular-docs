---
title: "Print and Export in Angular Linear Gauge component | Syncfusion"

component: "Linear Gauge"

description: "Learn here all about Print and Export feature of Syncfusion Angular Linear Gauge component and more."
---

# Print and Export in Angular Linear Gauge

## Print

<!-- markdownlint-disable MD013 -->

The rendered Linear Gauge can be printed directly from the browser by calling the [`print`](../api/linear-gauge/#print) method. To use the print functionality, set the [`allowPrint`](../api/linear-gauge/#allowprint) property as **true** and inject the **PrintService** in the **providers**.

{% tab template= "linear-gauge/print-and-export", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { PrintService, LinearGaugeComponent } from '@syncfusion/ej2-angular-lineargauge';
@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container" [allowPrint]=true #gauge>
    </ejs-lineargauge><div> <button  id='print' (click)='print()'>Print</button></div>`,
    providers: [PrintService]
})
export class AppComponent {
  @ViewChild('gauge')
  public gaugeObj: LinearGaugeComponent;
  print() {
    this.gaugeObj.print();
  };
}
```

{% endtab %}

## Export

### Image Export

<!-- markdownlint-disable MD013 -->

To use the image export functionality, set the [`allowImageExport`](../api/linear-gauge/#allowimageexport) property as **true** and inject the **ImageExportService** in the **providers**. The rendered Linear Gauge can be exported as an image using the [`export`](../api/linear-gauge/#export) method. This method requires two parameters: export type and file name. The Linear Gauge can be exported as an image with the following formats.

* JPEG
* PNG
* SVG

{% tab template= "linear-gauge/print-and-export", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { ImageExportService, LinearGaugeComponent } from '@syncfusion/ej2-angular-lineargauge';
@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container" [allowImageExport]=true #gauge>
    </ejs-lineargauge><div><button  id='export' (click)='export()'>Export</button></div>`,
    providers: [ImageExportService]
})
export class AppComponent {
    @ViewChild('gauge')
    public gaugeObj: LinearGaugeComponent;
    public export() {
      this.gaugeObj.export('PNG', 'Gauge');
    };
}
```

{% endtab %}

### PDF Export

To use the PDF export functionality, set the [`allowPdfExport`](../api/linear-gauge/#allowpdfexport) property as **true** and inject the **PdfExportService** in the **providers**. The rendered Linear Gauge can be exported as PDF using the [`export`](../api/linear-gauge/#export) method. The [`export`](../api/linear-gauge/#export) method requires three parameters: file type, file name and orientation of the PDF document. The orientation of the PDF document can be set as **Portrait** or **Landscape**.

{% tab template= "linear-gauge/print-and-export", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { PdfExportService, LinearGaugeComponent } from '@syncfusion/ej2-angular-lineargauge';
@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container" [allowPdfExport]=true #gauge>
    </ejs-lineargauge><div> <button  id='export' (click)='export()'>Export</button></div>`,
    providers: [PdfExportService]
})
export class AppComponent {
  @ViewChild('gauge')
  public gaugeObj: LinearGaugeComponent;
  public export(){
    this.gaugeObj.export('PDF', 'Gauge', 0);
  };
}
```

{% endtab %}

### Exporting Linear Gauge as base64 string of the file

The Linear Gauge can be exported as base64 string for the JPEG, PNG and PDF formats. The rendered Linear Gauge can be exported as base64 string of the exported image or PDF document used in the [`export`](../api/linear-gauge/#export) method. The arguments that are required for this method is export type, file name, orientation of the exported PDF document and **allowDownload** boolean value that is set as **false** to return base64 string. The value for the orientation of the exported PDF document is set as **null** for image export and **Portrait** or **Landscape** for the PDF document.

{% tab template= "linear-gauge/print-and-export", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { ImageExportService, LinearGaugeComponent } from '@syncfusion/ej2-angular-lineargauge';
@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container" [allowImageExport]=true #gauge>
    </ejs-lineargauge><div> <button  id='export' (click)='export()'>Export</button></div>`,
    providers: [ImageExportService]
})
export class AppComponent {
  @ViewChild('gauge')
  public gaugeObj: LinearGaugeComponent;
  public export(){
    const promise = this.gaugeObj.export('PNG', 'Gauge', null, false);
    promise.then((data)=>{
      document.writeln(data);
    })
  }
}
```

{% endtab %}

>The exporting of the Linear Gauge as base64 string is not applicable for the SVG format.