---
title: " Accumulation Chart Annotation | Angular "

component: "Accumulation Chart"

description: "The annotations are used to mark the specific area of interest in the chart area with texts, shapes or images."
---

# Annotation

The annotations are used to mark the specific area of interest in the chart area with texts, shapes or images.

<!-- markdownlint-disable MD033 -->

By using the <code>content</code> option of annotation property, you can specify the Id of the element that needs
to be displayed in the chart area.

{% tab template="chart/series/pie", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { pieData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container">
        <e-accumulation-annotations>
            <e-accumulation-annotation content='<div style="border: 1px solid black; background-color:#f5f5f5; padding: 5px 5px 5px 5px">3.5</div>'
             region='Series' coordinateUnits='Point' x='Feb' y=3.5>
            </e-accumulation-annotation>
        </e-accumulation-annotations>
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    ngOnInit(): void {
        this.piedata = pieData;

}
```

{% endtab %}

>Note: To use annotation feature in accumulation chart, we need to inject `AccumulationAnnotationService` into the `@NgModule.providers`.

## Region

The annotation can be placed with respect to either `Series` or `Chart`.

{% tab template="chart/series/pie", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { pieData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container">
        <e-accumulation-annotations>
            <e-accumulation-annotation content='<div style="border: 1px solid black;background-color:#f5f5f5; padding: 5px 5px 5px 5px">13.5</div>'
             region='Chart' coordinateUnits='Pixel' x=150 y=150>
            </e-accumulation-annotation>
        </e-accumulation-annotations>
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    ngOnInit(): void {
        this.piedata = pieData;

}
```

{% endtab %}

## Co-ordinate Units

Specifies the coordinate units of an annotation either in `Pixel` or `Point`.

{% tab template="chart/series/pie", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { pieData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container">
        <e-accumulation-annotations>
            <e-accumulation-annotation content='<div style="border: 1px solid black;background-color:#f5f5f5; padding: 5px 5px 5px 5px">Jan : 3</div>'
             region='Series' coordinateUnits='Point' x='Jan' y=3>
            </e-accumulation-annotation>
        </e-accumulation-annotations>
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    ngOnInit(): void {
        this.piedata = pieData;

}
```

{% endtab %}

## Alignment

The annotations provides the `verticalAlignment`or `horizontalAlignment` properties.
The `verticalAlignment` property can be customized via `Top`, `Bottom` or `Middle` and the `horizontalAlignment`
property can be customized via `Near`, `Far` or `Center`.

{% tab template="chart/series/pie", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { pieData } from 'datasource.ts';
@Component({
    selector: 'app-container',
    template:
    `<ejs-accumulationchart id="chart-container">
        <e-accumulation-annotations>
            <e-accumulation-annotation content='<div style="border: 1px solid black;background-color:#f5f5f5; padding: 5px 5px 5px 5px">Jan : 3</div>'
             region='Series' coordinateUnits='Point' x='Jan' y=3 verticalAlignment='Top' horizontalAlignment='Near'>
            </e-accumulation-annotation>
        </e-accumulation-annotations>
        <e-accumulation-series-collection>
            <e-accumulation-series [dataSource]='piedata' xName='x' yName='y'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ejs-accumulationchart>`
})
export class AppComponent implements OnInit {
    public piedata: Object[];
    ngOnInit(): void {
        this.piedata = pieData;

}
```

{% endtab %}