
# Print and Export

## Print

To use the print functionality, we should inject the `PrintService` into the `@NgModule.providers` and set the [`allowPrint`](../api/circular-gauge/#allowprint) property to **true**. The rendered circular gauge can be printed directly from the browser by calling the method [`print`](../api/circular-gauge/#print).

{% tab template="circulargauge/gauge-print-and-export", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { PrintService, CircularGaugeComponent } from '@syncfusion/ej2-angular-circulargauge';
@Component({
    selector: 'app-container',
    template:
    `<ejs-circulargauge id="circular-container" [allowPrint]=true #gauge>
    </ejs-circulargauge><div> <button id='print' (click)='print()'>Print</button></div>`,
    providers: [PrintService]
})
export class AppComponent implements OnInit {
    @ViewChild('gauge')
    public gaugeObj: CircularGaugeComponent;
    ngOnInit(): void {
        public print() {
            this.gaugeObj.print();
        };
    }
}

```

{% endtab %}

## Export

### Image Export

To use the image export functionality, we should inject the `ImageExportService` into the `@NgModule.providers` and set the [`allowImageExport`](../api/circular-gauge/#allowimageexport) property to **true**. The rendered circular gauge can be exported as an image using the [`export`](../api/circular-gauge/#export) method. The method requires two parameters: image type and file name. The circular gauge can be exported as an image in the following formats.

* JPEG
* PNG
* SVG

{% tab template="circulargauge/gauge-print-and-export", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { ImageExportService, CircularGaugeComponent } from '@syncfusion/ej2-angular-circulargauge';
@Component({
    selector: 'app-container',
    template:
    `<ejs-circulargauge id="circular-container" [allowImageExport]=true #gauge>
    </ejs-circulargauge><div> <button  id='export' (click)='export()'>Export</button></div>`,
    providers: [ImageExportService]
})
export class AppComponent implements OnInit {
    @ViewChild('gauge')
    public gaugeObj: CircularGaugeComponent;
    ngOnInit(): void {
        public export() {
            this.gaugeObj.export('PNG','Gauge');
        };
    }
}

```

{% endtab %}

We can get the image file as base64 string for the JPEG and PNG formats. The circular gauge can be exported to image as a base64 string using the [`export`](../api/circular-gauge/#export) method. There are four parameters required: image type, file name, orientation of the exported PDF document which must be set as **null** for image export and finally **allowDownload** which should be set as **false** to return base64 string.

{% tab template="circulargauge/gauge-print-and-export", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { ImageExportService, CircularGaugeComponent } from '@syncfusion/ej2-angular-circulargauge';
@Component({
    selector: 'app-container',
    template:
    `<ejs-circulargauge id="circular-container" [allowImageExport]=true #gauge>
    </ejs-circulargauge>
    <div><button  id='export' (click)='export()'>Export</button></div> <div id="data"></div>`,
    providers: [ImageExportService]
})
export class AppComponent implements OnInit {
    @ViewChild('gauge')
    public gaugeObj: CircularGaugeComponent;
    ngOnInit(): void {
        public export() {
            const promise = this.gaugeObj.export('PNG','Gauge',null,false);
            promise.then((data)=> {
                document.getElementById('data').innerHTML = data;
            })
        }
    }
}

```

{% endtab %}

### PDF Export

To use the PDF export functionality, we should inject the `PdfExportService` into the `@NgModule.providers` and set the [`allowPdfExport`](../api/circular-gauge/#allowpdfexport) property to **true**. The rendered circular gauge can be exported as PDF using the [`export`](../api/circular-gauge/#export) method. The [`export`](../api/circular-gauge/#export) method requires three parameters: file type, file name and orientation of the PDF document. The orientation setting is optional and "0" indicates portrait and "1" indicates landscape.

{% tab template="circulargauge/gauge-print-and-export", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import {PdfExportService, CircularGaugeComponent} from '@syncfusion/ej2-angular-circulargauge';
@Component({
    selector: 'app-container',
    template:
    `<ejs-circulargauge id="circular-container" [allowPdfExport]=true #gauge>
    </ejs-circulargauge><div> <button  id='export' (click)='export()'>Export</button></div>`,
    providers: [PdfExportService]
})
export class AppComponent implements OnInit {
    @ViewChild('gauge')
    public gaugeObj: CircularGaugeComponent;
    ngOnInit(): void {
        public export() {
            this.gaugeObj.export('PDF', 'Gauge', 0);
        };
    }
}

```

{% endtab %}

>Note: The exporting of the circular gauge as base64 string is not supported in the PDF export.