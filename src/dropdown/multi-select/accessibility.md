---
title: "Multiselect Accessibility"
component: "MultiSelect"
description: "This section for Syncfusion angular multiselect component explains the WAI-ARIA accessibility support."
---

# Accessibility

The MultiSelect component has been designed, keeping in mind the `WAI-ARIA` specifications, and applies
the WAI-ARIA roles, states, and properties along with `keyboard support`. This component is characterized
by complete keyboard interaction support and ARIA accessibility support that makes it easy for people who
use assistive technologies (AT) or those who completely rely on keyboard navigation.

## ARIA attributes

The MultiSelect component uses the `Listbox` role, and each list item has an `option` role. The following
`ARIA attributes` denote the MultiSelect state.

| **Properties** | **Functionalities** |
| --- | --- |
| aria-haspopup | Indicates whether the MultiSelect input element has a popup list or not. |
| aria-expanded | Indicates whether the popup list has expanded or not. |
| aria-selected | Indicates the selected option. |
| aria-readonly | Indicates the readonly state of the MultiSelect element. |
| aria-disabled | Indicates whether the MultiSelect component is in a disabled state or not. |
| aria-activedescendent | This attribute holds the ID of the active list item  to focus its descendant child element. |
| aria-owns | This attribute contains the ID of the popup list to indicate popup as a child element. |

## Keyboard interaction

You can use the following key shortcuts to access the MultiSelect without interruptions.

| **Keyboard shortcuts** | **Actions** |
| --- | --- |
| <kbd>Arrow Down</kbd> | Set focus at the first item in the MultiSelect when no item selected. Otherwise, moves focus next to the currently selected item. |
| <kbd>Arrow Up</kbd> | Moves focus previous to the currently selected one. |
| <kbd>Page Down</kbd> | Scrolls down to the next page and set focus to the first item when popup list opens. |
| <kbd>Page Up</kbd> | Scrolls up to the previous page and set focus to the first item when popup list opens. |
| <kbd>Enter</kbd> | Selects the focused item, and when it is in an close state the popup list opens. |
| <kbd>Tab</kbd> | Focuses on the next TabIndex element on the page when the popup is closed. Otherwise, closes the popup list and remains the focus of the component. |
| <kbd>Shift + tab </kbd> | Focuses on the previous TabIndex element on the page when the popup is closed. Otherwise, closes the popup list and remains the focus of the component. |
| <kbd>Alt + Down</kbd> | Opens the popup list. |
| <kbd>Alt + Up</kbd> | Closes the popup list. |
| <kbd>Esc(Escape)</kbd> | Closes the popup list when it is in an open state and the currently selected item remains the same. |
| <kbd>Home</kbd> | set focus to the first item. |
| <kbd>End</kbd> | set focus to the last item. |

> In the below sample, focus the MultiSelect component using <kbd>alt+t</kbd> keys.

{% tab template="multiselect/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component, HostListener,ViewChild } from '@angular/core';
import { MultiSelectComponent } from '@syncfusion/ej2-angular-dropdowns';
@Component({
    selector: 'app-root',
    // specifies the template string for the MultiSelect component
    template: `<ejs-multiselect id='multiselectelement' #samples [dataSource]='gameList' [fields]='fields'[placeholder]='placeholder' [popupHeight]='height'></ejs-multiselect>`
})
export class AppComponent {
    @ViewChild('samples')
    public sports: MultiSelectComponent;
    constructor() {
    }
    //set the data to dataSource property
    public gameList: Object[] =  [
        { id: 'Game1', game: 'Badminton' },
        { id: 'Game2', game: 'Basketball' },
        { id: 'Game3', game: 'Cricket' },
        { id: 'Game4', game: 'Football' },
        { id: 'Game5', game: 'Golf' }
    ];
    // maps the appropriate column to fields property
    public fields: Object = { text: 'game', value: 'id' };
    // set the popup list height
    public height: string = '200px';
    // set placeholder to MultiSelect input element
    public placeholder: string = 'Select games';
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