---
title: "Auto Close"
component: "Sidebar"
description: "Sidebar can be initialized in expand or collapsed state in user specified resolutions."
---

# Auto-close

The Sidebar often behaves differently on mobile display and differently on desktop display.
It has an effective feature that offers to set it in opened or closed state depending on the specified screen resolution.
This functionality can be achieved through [`mediaQuery`](../api/sidebar/#mediaquery) property that allows you to set the Sidebar in an expanded state
 or collapsed state only in user-defined resolution.

> window.matchMedia() method returns the object of parsed `media query` string.
The value of matchMedia() can be any of the media features of CSS @media rule. For example, min-width and max-width.

{% tab template="sidebar/autoclose", isDefaultActive = "true",sourceFiles="app/**/*.ts,app/app.component.html,app/app.component.css" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    styleUrls: ['app/app.component.css'],
    templateUrl: 'app/app.component.html'
})
export class AppComponent {
    public width: string = '280px';
    public mediaQuery: object = window.matchMedia('(min-width: 600px)');
}

```

{% endtab %}

* In the following sample,the Sidebar will be in expanded state only in resolution below `400px`.

> `max-width` is one of media feature which represents maximum with of display area such as width of the view port.

{% tab template="sidebar/autoclose", isDefaultActive = "true",sourceFiles="app/**/*.ts,app/app.component.html, app/app.component.css" %}

```typescript

import { Component } from '@angular/core';
@Component({
    selector: 'app-root',
    styleUrls: ['app/app.component.css'],
    templateUrl: 'app/app.component.html'
})
export class AppComponent {
    public width: string = '280px';
    public mediaQuery: object = window.matchMedia('(max-width: 400px)');
}

```

{% endtab %}