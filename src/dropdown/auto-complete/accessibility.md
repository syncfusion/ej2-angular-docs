---
title: "Autocomplete Accessibility"
component: "AutoComplete"
description: "This section explains the WAI-ARIA accessibility support of the Syncfusion angular autocomplete component."
---

# Accessibility

The AutoComplete component has been designed, keeping in mind the `WAI-ARIA` specifications,
and applies the `WAI-ARIA` roles, states, and properties along with `keyboard support`.
This component is characterized by complete keyboard interaction support and ARIA
accessibility support that makes it easy for people who
use assistive technologies (AT) or those who completely rely on keyboard navigation.

## ARIA attributes

The AutoComplete component uses the `combobox` role and each list item has an `option` role. The following
`ARIA Attributes` denote the AutoComplete state.

| **Property** | **Functionalities** |
| --- | --- |
| aria-haspopup | Indicates whether the AutoComplete input element has a suggestion list or not. |
| aria-expanded | Indicates whether the suggestion list has expanded or not. |
| aria-selected | Indicates the selected option from the list. |
| aria-readonly | Indicates the readonly state of the AutoComplete element. |
| aria-disabled | Indicates whether the AutoComplete component is in a disabled state or not.|
| aria-activedescendent | This attribute holds the ID of the active list item to focus its descendant child element. |
| aria-owns | This attribute contains the ID of the suggestion list to indicate popup as a child element. |
| aria-autocomplete | This attribute contains the ‘both’ to a list of options shows and the currently selected suggestion also shows inline. |

## Keyboard interaction

You can use the following key shortcuts to access the AutoComplete without interruptions.

| **Keyboard shortcuts** | **Actions** |
| --- | --- |
| <kbd>Arrow Down</kbd> | In popup hidden state, opens the suggestion list. In popup open state, selects the first item when no item selected else selects the item next to the currently selected item. |
| <kbd>Arrow Up</kbd> | In popup hidden state, opens the suggestion list. In popup open state, selects the last item when no item selected else selects the item previous to the currently selected one. |
| <kbd>Page Down</kbd> | Scrolls down to the next page and selects the first item when popup list opens. |
| <kbd>Page Up</kbd> | Scrolls up to previous page and select the first item when popup list open. |
| <kbd>Enter</kbd> | Selects the focused item and set to AutoComplete component. |
| <kbd>Tab</kbd> | Focuses on the next tab indexed element when the popup is closed. Otherwise, closes the popup list and remains the focus in component suppose if it is in an open state. |
| <kbd>Shift + tab </kbd> | Focuses the previous tab indexed element when the popup is closed.  Otherwise,closes the popup list and remains the focus in component suppose if it is in an open state. |
| <kbd>Alt + Down</kbd> | Opens the popup list. |
| <kbd>Alt + Up</kbd> | In popup hidden state, opens the popup list. In popup open state, closes the popup list. |
| <kbd>Esc(Escape)</kbd> | Closes the popup list when it is in an open state then remove the selection. |
| <kbd>Home</kbd> | Cursor moves to before of first character in input. |
| <kbd>End</kbd> | Cursor moves to next of last character in input. |

> In the below sample, focus the AutoComplete component using <kbd>alt+t</kbd> keys.

{% tab template="autocomplete/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, HostListener, ViewChild } from '@angular/core';
import { AutoCompleteComponent } from '@syncfusion/ej2-angular-dropdowns';
@Component({
    selector: 'app-root',
    // specifies the template string for the AutoComplete component
    template: `<ejs-autocomplete id='atcelement' #samples [dataSource]='sportsData' [fields]='fields' [placeholder]='text'></ejs-autocomplete>`
})
export class AppComponent {
    @ViewChild('samples')
    public sports: AutoCompleteComponent;
    constructor() {
    }
    public sportsData:{ [key: string]: Object }[] = [
        { Id: 'Game1', Game: 'Badminton' },
        { Id: 'Game2', Game: 'Basketball' },
        { Id: 'Game3', Game: 'Cricket' },
        { Id: 'Game4', Game: 'Football' },
        { Id: 'Game5', Game: 'Golf' },
        { Id: 'Game6', Game: 'Hockey' },
        { Id: 'Game7', Game: 'Rugby' },
        { Id: 'Game8', Game: 'Snooker' },
        { Id: 'Game9', Game: 'Tennis' }
    ];
    // maps the appropriate column to fields property
    public fields: Object ={ value: 'Game' };
    //set the placeholder to AutoComplete input
    public text: string = "Find a game";
    @HostListener('document:keyup', ['$event'])
    handleKeyboardEvent(event: KeyboardEvent) {
        if (event.altKey && event.keyCode === 84 /* t */) {
            // press alt+t to focus the control.
            this.sports.focusIn();
        }
    }
}

```

{% endtab %}