---
title: "Action Buttons"
component: "Card"
description: "This section explains how to customizes the card using action buttons and changes the vertical or horizontal alignment of the card element."
---

# Action Buttons

You can include Action buttons within the Card and customize them. Action button is a `div`
element with `e-card-actions` class followed by button tag or anchor tag within the card root element.

* For adding action buttons you can create button or anchor tag with `e-card-btn` class within the card action element.

```html
    <div class = "e-card">
        <div class="e-card-actions">
            <button class="e-card-btn"></button>
            <a href="#"></a>
        </div>
    </div>
```

## Vertical

By default, action buttons positioned in horizontal alignment , and also it can be aligned to show in vertical alignment by adding
`e-card-vertical` class.

```html
    <div class = "e-card">
        <div class="e-card-actions e-card-vertical">
            <button class="e-card-btn">More</button>
            <a href="#">Share</a>
        </div>
    </div>
```

{% tab template="card/card_action_btn", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
   <div style="margin: 50px;">
        <div class="e-card" style="max-width:400px">
            <div class="e-card-header-title">Eiffel Tower</div>
            <div class="e-card-content">
               The Eiffel Tower is acknowledged as the universal symbol of Paris and France.
            </div>
            <div class="e-card-actions">
                <button  class="e-card-btn">
                    <img src="./fav.png" style="height: 18px;width: 18px;" title="Bookmark">
                </button>
                <button class="e-card-btn">
                    <img src="./like.png" style="height: 18px;width: 18px;" title="Like">
                </button>
                <button class="e-card-btn">
                    <img src="./share.png" style="height: 18px;width: 18px;" title="Share">
                </button>
            </div>
        </div>
    </div>
    <div style="margin-left: 50px;">
            <div class="e-card" style="max-width:400px">
                <div class="e-card-header-title">Eiffel Tower</div>
                <div class="e-card-content">
                    The Eiffel Tower is acknowledged as the universal symbol of Paris and France.
                </div>
                <div class="e-card-actions e-card-vertical">
                    <button class="e-card-btn">LIKE</button>
                    <button class="e-card-btn">SHARE</button>
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

## See Also

* [How to integrate other component inside the card](./how-to/integrate-other-component-inside-the-card)