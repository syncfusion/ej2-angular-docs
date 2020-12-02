---
title: "Horizontal Card"
component: "Card"
description: "This section explains how to align the Essential JS 2 cards vertically and differentiate from horizontal layout."
---

# Horizontal Card

By default, all the card elements are aligned vertically one after the other as in the DOM.
 You can achieve the element to align horizontally as well by adding the class `e-card-horizontal` in the root card element.

## Stacked cards

* An horizontally aligned card can push a specific column to align vertical using `e-card-stacked` class.
 This will align the stacked section vertically aligned differentiating from horizontal layout.

Class   | Description
------------ | -------------
`e-card-horizontal` | To align card elements horizontally.
`e-card-stacked` | To align elements vertically within the horizontal layout.

```html
        <div tabindex="0" class="e-card e-card-horizontal">
            <img src="code1.png" alt="Sample">   --> Aligned in horizontal
            <div class="e-card-stacked">         --> Aligned in horizontal
               // Inside the element all are aligned vertical directions
            </div>
        </div>
```

{% tab template="card/card_horizontal", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <div style="margin: 50px;display: flex;flex-direction: row;justify-content: center;">
        <div tabindex="0" class="e-card e-card-horizontal" style="width:400px">
            <img src="./Code.png" alt="Sample" style="height: 180px">
            <div class="e-card-stacked">
                <div class="e-card-header">
                    <div class="e-card-header-caption">
                        <div class="e-card-header-title">Philips Trimmer</div>
                    </div>
                </div>
                <div class="e-card-content">
                    Powered by the innovative DuraPower Technology which optimizes power consumption, Philips trimmers are designed to last longer
                    than 4 ordinary trimmers.
                </div>
            </div>
        </div>
    </div>
        `
})

export class AppComponent {
    @ViewChild('element') element;

}
```

{% endtab %}