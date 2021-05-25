---
title: "Customize selected tab styles"
component: "Tab"
description: "This example demonstrates how to customize selected tab header styles in the Essential JS 2 Tab control."
---

# Customize selected tab styles

You can customize the Tab style by overriding its header and active tab CSS classes. Define HTML string for adding
animation and customizing the Tab header and pass it to [`text`](../../api/tab/header#text) property. Now you can
override the style using custom CSS classes added to the Tab elements.

> You can add the custom class into Tab component using [`cssClass`](../../api/toolbar/item#cssclass)
property which is used to customize the Tab component.

{% tab template="tab/custom-styles", sourceFiles="app/**/*.ts,index.css"%}

```typescript

import { Component } from '@angular/core';

/**
 * Customize selected tab styles
 */

@Component({
    selector: 'app-container',
    template: `<ejs-tab id="element" [items]='items'></ejs-tab>`
})
export class AppComponent {
    public items: Object[] = [
        {
            header: { 'text': '<div><div class="e-image e-andrew"></div><div class="e-title fade-in">Andrew</div></div>' },
            content: 'Andrew received his BTS commercial in 1974 and a Ph.D. in international marketing from the University of Dallas in 1981.He is fluent in French and Italian and reads German.He joined the company as a sales representative, was promoted to sales manager in January 1992 and to vice president of sales in March 1993.Andrew is a member of the Sales Management Roundtable, the Seattle Chamber of Commerce, and the Pacific Rim Importers Association.'
        },
        {
            header: { 'text': '<div><div class="e-image e-margaret"></div><div class="e-title fade-in">Margaret</div></div>' },
            content: 'Margaret holds a BA in English literature from Concordia College (1958) and an MA from the American Institute of Culinary Arts (1966).She was assigned to the London office temporarily from July through November 1992.'
        },
        {
            header: { 'text': '<div><div class="e-image e-janet"></div><div class="e-title fade-in">Janet</div></div>' },
            content: 'Janet has a BS degree in chemistry from Boston College (1984).She has also completed a certificate program in food retailing management.Janet was hired as a sales associate in 1991 and promoted to sales representative in February 1992.'
        }
    ]
}

```

{% endtab %}
