# Annotations

<!-- markdownlint-disable MD010 -->

Annotations are used to mark a specific area of interest in the gauge with texts, shapes or images.

## Content

You can place any custom element on the axis area by assigning the id of the element to
[`content`](../api/circular-gauge/annotation/#content-string) property of
[`annotation`](../api/circular-gauge/annotation) object.

>Note: To use annotation feature, we need to inject `AnnotationsService` into the `NgModule.providers`.

{% tab template="circulargauge/gauge-annotations", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-circulargauge id="circular-container">
        <e-axes>
            <e-axis>
                <e-pointers>
                    <e-pointer value = 50></e-pointer>
                </e-pointers>
                <e-annotations>
                    <e-annotation zIndex="1">
						<ng-template #content>
							<div>
							  <div><span>Pointer Value : 50</span>
                              </div>
                            </div>
                        </ng-template>
                    </e-annotation>
                </e-annotations>
            </e-axis>
        </e-axes>
    </ejs-circulargauge>`
})
export class AppComponent implements OnInit {
    ngOnInit(): void {
    }
}

```

{% endtab %}

## Position

Annotation can be placed around the axis by using [`radius`](../api/circular-gauge/annotation/#radius-string)
and [`angle`](../api/circular-gauge/annotation/#angle-number) property.
For example, if the angle is 90 degree and the radius is 110%, then the annotation, will be placed at the right side of the axis.

Radius of the annotation takes value either in pixel or percentage.
By setting value in percentage, annotation gets its position with respect to its axis radius.

{% tab template="circulargauge/gauge-annotations", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-circulargauge id="circular-container">
        <e-axes>
            <e-axis>
                <e-pointers>
                    <e-pointer value = 50></e-pointer>
                </e-pointers>
                <e-annotations>
                    <e-annotation angle=90 radius="150%" zIndex="1">
						<ng-template #content>
							<div>
								<div><span>Pointer Value : 50</span>
                                </div>
                            </div>
                        </ng-template>
                    </e-annotation>
                </e-annotations>
            </e-axis>
        </e-axes>
    </ejs-circulargauge>`
})
export class AppComponent implements OnInit {
    ngOnInit(): void {
        // Initialize objects
    }
}

```

{% endtab %}

## Sub Gauge

As the annotation allows you to place any custom element,
we can initialize a gauge to the element and can be used to place that in another gauge.

{% tab template="circulargauge/gauge-annotations", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { CircularGauge } from '@syncfusion/ej2-angular-circulargauge';
import { ILoadedEventArgs } from '@syncfusion/ej2-circulargauge';

@Component({
    selector: 'app-container',
    template:
    `<ejs-circulargauge id="circular-container" (loaded)='loaded($event)'>
        <e-axes>
            <e-axis minimum=0 maximum=12 startAngle=0 endAngle=360 [lineStyle]="lineStyle" [labelStyle]="labelStyle">
                <e-annotations>
                    <e-annotation angle=270 radius='40%'>
                    <ng-template #content>
                      <div id="subGauge" style="width:90px;height:90px"></div>
                    </ng-template>
                    </e-annotation>
                    <e-annotation angle=90 radius='40%'>
                    <ng-template #content>
                      <div id="subTime" style="width:90px;height:90px">
                        <span>6:30 PM</span>
                      </div>
                    </ng-template>
                    </e-annotation>
                </e-annotations>
                <e-ranges>
                    <e-range start=0 end=3 color="rgba(29,29,29,0.7)"></e-range>
                    <e-range start=3 end=12 color="rgba(168,145,102,0.1)"></e-range>
                </e-ranges>
                <e-pointers>
                    <e-pointer pointerWidth=5 radius="40%" value=6.5 color="#1d1d1d" [border]='pointerBorder' [cap]='pointerCap' [needleTail]='pointerTail' [animation]='pointerAnimation'></e-pointer>
                    <e-pointer pointerWidth=5 radius="60%" value=6 color="#1d1d1d" [border]='pointerBorder' [cap]='pointerCap' [needleTail]='pointerTail' [animation]='pointerAnimation'></e-pointer>
                    <e-pointer pointerWidth=5 radius="70%" value=9.8 color="#a89166" [cap]='pointerCap1' [needleTail]='pointerTail1' [animation]='pointerAnimation'></e-pointer>
                </e-pointers>
            </e-axis>
        </e-axes>
    </ejs-circulargauge>`
})
export class AppComponent implements OnInit {
    public labelStyle: object;
    public lineStyle: object;
    public pointerBorder: object;
    public pointerCap: object;
    public pointerTail: object;
    public pointerAnimation: object;
    public pointerCap1: object;
    public pointerTail1: object;
    public loaded: Function;
    ngOnInit(): void {
        // Initialize objects
        this.labelStyle = {
            hiddenLabel: 'First'
        };
        this.lineStyle = {
            width: 0
        };
        this.pointerBorder= { width: 1, color: 'rgb(29,29,29)' };
        this.pointerCap= {
            color: 'rgb(29,29,29)',
            radius: 0,
            border: {
                width: 0.2,
                color: 'red'
            }
        };
        this.pointerTail= {
            length: '0%'
        };
        this.pointerAnimation= {
            enable: false
        };
        this.pointerCap1= {
            color: 'rgba(168,145,102,1)',
            radius: 4,
            border: {
                width: 0.2,
                color: 'rgba(168,145,102,1)'
            }
        };
        this.pointerTail1= {
            color: 'rgba(168,145,102,1)',
            length: '20%'
        };
        this.loaded = (args: ILoadedEventArgs): void {
            let gauge: CircularGauge = new CircularGauge({
                axes: [{
                    minimum: 0,
                    maximum: 12,
                    startAngle: 0,
                    endAngle: 360,
                    majorTicks:{ interval: 3 },
                    lineStyle: { width: 0 },
                    ranges: [{
                        start: 0, end: 3,
                        startWidth: 5, endWidth: 5,
                        color: 'rgba(29,29,29,0.7)'
                    }, {
                        start: 3, end: 12,
                        startWidth: 5, endWidth: 5,
                        color: 'rgba(168,145,102,0.1)'
                    }],
                    labelStyle: {
                        hiddenLabel: 'First',
                        offset: -5
                    },
                    pointers: [{
                        pointerWidth: 2,
                        radius: '40%',
                        color: 'rgb(29,29,29)',
                        border: { width: 1, color: 'rgb(29,29,29)' },
                        cap: {
                            color: 'rgb(29,29,29)',
                            radius: 2,
                            border: {
                                width: 0.2,
                                color: 'red'
                            }
                        },
                        needleTail: {
                            length: '0%'
                        }, animation: {
                            enable: false
                        }
                    }]
                }]
            }, '#subGauge');
        }
    }
}

```

{% endtab %}

## See also

* [Tooltip for Annotation](https://ej2.syncfusion.com/angular/documentation/circular-gauge/gauge-user-interaction/#tooltip-for-annotations/)
