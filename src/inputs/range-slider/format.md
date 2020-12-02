---
title: "Slider Formatting"
component: "Slider"
description: "Angular slider supports formatting to customize slider values like time, currency & km, values, also displayed in ticks & tooltip."
---

# Formatting

The `format` feature used to customize the units of Slider values to desired format. The formatted values will also be applied
to the ARIA attributes of the slider. There are two ways of achieving formatting in slider.

* Use the format API of slider which utilizes our [Internationalization](../common/internationalization/) to format values.

* Customize using the events namely `renderingTicks` and `tooltipChange`.

{% tab template="slider/format-01", sourceFiles="app/**/*,index.css", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'my-app',
    templateUrl: 'app/template.html',
    styleUrls:['index.css']
})

export class AppComponent {
    public tooltipData: Object = { isVisible: true, format: 'C2' };
    public ticksData: Object = { placement: 'After', format: 'C2', largeStep: 20, smallStep: 10, showSmallTicks: true };
}

```

{% endtab %}

## Using format API

In this method, we have different predefined formatting styles like Numeric (N), Percentage (P), Currency (C) and `#` specifiers. In
this below example, we have formatted the `ticks` and `tooltip` values into percentage.

{% tab template="slider/format-02", sourceFiles="app/**/*,index.css", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'my-app',
    templateUrl: 'app/template.html',
    styleUrls:['index.css']
})

export class AppComponent {
    public tooltipData: Object = { placement: 'Before', isVisible: true, showOn: 'Always', format: 'P0' };
    public ticksData: Object = { placement: 'After', largeStep: .2, smallStep: .1, showSmallTicks: true, format: 'P0' };

}

```

{% endtab %}

## Using Events

In this method, we will be retrieving the values from the slider events then process them to desired formatted the values.
In this sample we have customized the `ticks` values into weekdays as one formatting and `tooltip` values into day of the week as another formatting.

{% tab template="slider/format-03", sourceFiles="app/**/*,index.css", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'my-app',
    templateUrl: 'app/template.html',
    styleUrls:['index.css']
})

export class AppComponent {
    public tooltipData: Object = { placement: 'Before', isVisible: true };
    public ticksData: Object = { placement: 'After', largeStep: 1 };

    tooltipChangeHandler(args: SliderTooltipEventArgs): void {
        // Weekdays Array
        let daysArr: string [] = ['Sunday','Monday','Tuesday','Wednesday','Thrusday','Friday','Saturday'];
        // Customizing each ticks text into weeksdays
        args.text = daysArr[parseFloat(args.value)];
    }

    renderingTicksHandler(args: SliderTickEventArgs): void {
        // Customizing tooltip to display the Day (in numeric) of the week
        args.text =  'Day ' + (Number(args.value) + 1).toString();
    }
}

```

{% endtab %}
