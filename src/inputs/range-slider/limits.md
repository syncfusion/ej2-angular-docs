---
title: "Slider Limits"
component: "Slider"
description: "Angular slider component supports limits feature that restricts thumb movement in min & max values and also supports interval dragging between range values."
---

# Movement Limits and Drag Interval

The slider limits restrict the slider thumb between a particular range. This is used if higher or lower value affects the process
or product where the slider is being used.

The following are the six options in the slider's limits object. Each API in the limits object is optional.

* ``enabled``: Enables the limits in the Slider.
* ``minStart``: Sets the minimum limit for the first handle.
* ``minEnd``: Sets the maximum limit for the first handle.
* ``maxStart``: Sets the minimum limit for the second handle.
* ``maxEnd``: Sets the maximum limit for the second handle.
* ``startHandleFixed``: Locks the first handle.
* ``endHandleFixed``: Locks the second handle.

## Default and MinRange Slider limits

There is only one handle in the Default and MinRange Slider, so ``minStart``, ``minEnd``, and ``startHandleFixed`` options can be used.
When the limits are enabled in the Slider, the limited area becomes darken. So you can differentiate the allowed and restricted area.
Refer to the following snippet to enable the limits in the Slider.

```typescript

    ......

    limits: { enabled: true, minStart: 10, minEnd: 40 }

    ......

```

{% tab template="slider/default-limit", sourceFiles="app/**/*,index.css", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'my-app',
    templateUrl: 'app/template.html',
    styleUrls:['index.css']
})

export class AppComponent {
  public type: string ="MinRange";
  public value: number = 30;
  public tooltip: object= { isVisible: true };
  public min: number = 0;
  public max: number = 100;
  public limits: object = { enabled: true, minStart: 10, minEnd: 40 };
}

```

{% endtab %}

## Range Slider limits

In the range slider, both handles can be restricted and locked from the limit's object. In this sample, the first handle is limited between
10 and 40, and the second handle is limited between 60 and 90.

```typescript

    ......

    limits: { enabled: true, minStart: 10, minEnd: 40, maxStart: 60, maxEnd: 90 }

    ......

```

{% tab template="slider/range-limit", sourceFiles="app/**/*,index.css", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'my-app',
    templateUrl: 'app/template.html',
    styleUrls:['index.css']
})

export class AppComponent {
  public type: string ="Range";
  public value: number[] = [30, 70];
  public tooltip: object= { isVisible: true };
  public min: number = 0;
  public max: number = 100;
  public limits: object = { enabled: true, minStart: 10, minEnd: 40, maxStart: 60, maxEnd: 90 };
}

```

{% endtab %}

## Handle lock

The movement of slider handles can be locked by enabling the ``startHandleFixed`` and ``endHandleFixed`` properties in the limit's object.
In this sample, the movement of both slider handles has been locked.

```typescript
    ......

    limits: { enabled: true, startHandleFixed: true, endHandleFixed: true }

    ......

```

{% tab template="slider/handle-lock", sourceFiles="app/**/*,index.css", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'my-app',
    templateUrl: 'app/template.html',
    styleUrls:['index.css']
})

export class AppComponent {
  public type: string ="Range";
  public value: number[] = [30, 70];
  public tooltip: object= { isVisible: true };
  public min: number = 0;
  public max: number = 100;
  public limits: object = { enabled: true, startHandleFixed: true, endHandleFixed: true };
}

```

{% endtab %}
