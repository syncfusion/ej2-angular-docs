# Accumulation Chart Types

<!-- markdownlint-disable MD036 -->

## Pyramid Chart

To render a pyramid series, use series [`type`](../api/accumulation-chart/accumulationSeries/#type) as `Pyramid`.

{% tab template="chart/series/pyramid", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ej-accumulationchart id="chart-container">
        <e-accumulation-series-collection>
            <e-accumulation-series width='400px' type='Pyramid' [dataSource]='pyramidData' xName='x' yName='y' [dataLabel]='datalabel'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ej-accumulationchart>`
})
export class AppComponent implements OnInit {
    public pyramidData: Object[];
    public datalabel: Object;
    public enableSmartLabels: boolean;
    ngOnInit(): void {
        this.datalabel = { visible: true, name: 'text', position: 'Inside' };
        this.enableSmartLabels = true;
        this.pyramidData = [
                { x: 'Australia', y: 20, text: 'Australia 20%' },
                { x: 'France', y: 22, text: 'France 22%' },
                { x: 'China', y: 23, text: 'China 23%' },
                { x: 'India', y: 24, text: 'India 24%' },
                { x: 'Japan', y: 25, text: 'Japan 25%' },
                { x: 'Germany', y: 27, text: 'Germany 27%' }];
    }

}

```

{% endtab %}

## Funnel Chart

To render a funnel series, use series [`type`](../api/accumulation-chart/accumulationSeries/#type) as `Funnel`.

{% tab template="chart/series/funnel", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ej-accumulationchart id="chart-container">
        <e-accumulation-series-collection>
            <e-accumulation-series width='330px' type='Funnel' [dataSource]='funneldata' xName='x' yName='y' [dataLabel]='datalabel'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ej-accumulationchart>`
})
export class AppComponent implements OnInit {
    public funneldata: Object[];
    public datalabel: Object;
    public enableSmartLabels: boolean;
    ngOnInit(): void {
        this.datalabel = { visible: true, name: 'text', position: 'Inside' };
        this.enableSmartLabels = true;
        this.funneldata = [
                { x: 'Renewed', y: 18.20, text: 'Renewed 18.20%' },
                { x: 'Subscribe', y: 27.3, text: 'Subscribe 27.3%' },
                { x: 'Support', y: 55.9, text: 'Support 55.9%' },
                { x: 'Downloaded', y: 76.8, text: 'Downloaded 76.8%' },
                { x: 'Visited', y: 100, text: 'Visited 100%' }];
    }

}

```

{% endtab %}

## Customization of Accumulation Chart

## Size

Accumulation chart provides options to customize the size of the funnel or pyramid chart by using the  `width` and `height` property.

{% tab template="chart/series/funnel", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ej-accumulationchart id="chart-container">
        <e-accumulation-series-collection>
            <e-accumulation-series width='330px' type='Funnel' [dataSource]='funneldata' xName='x' yName='y' [dataLabel]='datalabel'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ej-accumulationchart>`
})
export class AppComponent implements OnInit {
    public funneldata: Object[];
    public datalabel: Object;
    public enableSmartLabels: boolean;
    ngOnInit(): void {
        this.datalabel = { visible: true, name: 'text', position: 'Inside' };
        this.enableSmartLabels = true;
        this.funneldata = [
                { x: 'Renewed', y: 18.20, text: 'Renewed 18.20%' },
                { x: 'Subscribe', y: 27.3, text: 'Subscribe 27.3%' },
                { x: 'Support', y: 55.9, text: 'Support 55.9%' },
                { x: 'Downloaded', y: 76.8, text: 'Downloaded 76.8%' },
                { x: 'Visited', y: 100, text: 'Visited 100%' }];
    }

}

```

{% endtab %}

## Neck Size

The funnel neck size can be customized by using the `neckWidth` and `neckHeight` property.

{% tab template="chart/series/funnel", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ej-accumulationchart id="chart-container">
        <e-accumulation-series-collection>
            <e-accumulation-series width='330px' type='Funnel' [dataSource]='funneldata' xName='x' yName='y' [dataLabel]='datalabel' [neckWidth]='neckWidth'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ej-accumulationchart>`
})
export class AppComponent implements OnInit {
    public funneldata: Object[];
    public datalabel: Object;
    public enableSmartLabels: boolean;
    public neckWidth: string = '5%';

    ngOnInit(): void {
        this.datalabel = { visible: true, name: 'text', position: 'Inside' };
        this.enableSmartLabels = true;
        this.funneldata = [
                { x: 'Renewed', y: 18.20, text: 'Renewed 18.20%' },
                { x: 'Subscribe', y: 27.3, text: 'Subscribe 27.3%' },
                { x: 'Support', y: 55.9, text: 'Support 55.9%' },
                { x: 'Downloaded', y: 76.8, text: 'Downloaded 76.8%' },
                { x: 'Visited', y: 100, text: 'Visited 100%' }];
    }

}

```

{% endtab %}

## Gap between the segments

The space between the segments can be customized by using the `gapRatio` option of the series and
it is applicable for pyramid and funnel chart. It ranges from 0 to 1.

{% tab template="chart/series/funnel", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ej-accumulationchart id="chart-container">
        <e-accumulation-series-collection>
            <e-accumulation-series width='330px' type='Funnel' [dataSource]='funneldata' xName='x' yName='y' [dataLabel]='datalabel' [gapRatio]="gapRatio"></e-accumulation-series>
        </e-accumulation-series-collection>
    </ej-accumulationchart>`
})
export class AppComponent implements OnInit {
    public funneldata: Object[];
    public datalabel: Object;
    public enableSmartLabels: boolean;
    public gapRatio: number = 0.03;

    ngOnInit(): void {
        this.datalabel = { visible: true, name: 'text', position: 'Inside' };
        this.enableSmartLabels = true;
        this.funneldata = [
                { x: 'Renewed', y: 18.20, text: 'Renewed 18.20%' },
                { x: 'Subscribe', y: 27.3, text: 'Subscribe 27.3%' },
                { x: 'Support', y: 55.9, text: 'Support 55.9%' },
                { x: 'Downloaded', y: 76.8, text: 'Downloaded 76.8%' },
                { x: 'Visited', y: 100, text: 'Visited 100%' }];
    }

}

```

{% endtab %}

## Pyramid mode

Pyramid chart supports linear and surface modes of rendering. The default `pyramidMode` type is `linear`.

{% tab template="chart/series/pyramid", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ej-accumulationchart id="chart-container">
        <e-accumulation-series-collection>
            <e-accumulation-series width='400px' type='Pyramid' pyramidMode='Linear' [dataSource]='pyramidData' xName='x' yName='y' [dataLabel]='datalabel'></e-accumulation-series>
        </e-accumulation-series-collection>
    </ej-accumulationchart>`
})
export class AppComponent implements OnInit {
    public pyramidData: Object[];
    public datalabel: Object;
    public enableSmartLabels: boolean;
    ngOnInit(): void {
        this.datalabel = { visible: true, name: 'text', position: 'Inside' };
        this.enableSmartLabels = true;
        this.pyramidData = [
                { x: 'Australia', y: 20, text: 'Australia 20%' },
                { x: 'France', y: 22, text: 'France 22%' },
                { x: 'China', y: 23, text: 'China 23%' },
                { x: 'India', y: 24, text: 'India 24%' },
                { x: 'Japan', y: 25, text: 'Japan 25%' },
                { x: 'Germany', y: 27, text: 'Germany 27%' }];
    }
}

```

{% endtab %}