---
title: "Localization"
component: "Dialog"
description: "Explains how to localize the static text (built-in text) content of the dialog control such as close button's tooltip text."
---

# Localization

Localization library allows to localize the default text content of
Dialog. In Dialog, The close button's tooltip text alone will be localize based on culture.

| Locale key | en-US (default)  |
|------|------|
| close |  Close |

## Loading translations

To load translation object in an application use `load` function of `L10n` class.

In the below sample, `French` culture is set to Dialog and change the close button's tooltip
text.

{% tab template="dialog/getting-started", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript
import { Component, ViewChild, OnInit, ElementRef } from '@angular/core';
import { DialogComponent } from '@syncfusion/ej2-angular-popups';
import { L10n } from '@syncfusion/ej2-base';
import { EmitType } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    template: `
    <button class="e-control e-btn" style="position: absolute;" id="targetButton" (click)="onOpenDialog($event)">Open Dialog</button>
    <div #container class='root-container'></div>
      <ejs-dialog id='dialog' #ejDialog locale='fr-BE' showCloseIcon='true' header='Dialogue' content='Dialogue avec la culture française' [target]='targetElement' width='250px'>
      </ejs-dialog>
        `
})

export class AppComponent implements OnInit {
    @ViewChild('ejDialog') ejDialog: DialogComponent;
   // Create element reference for dialog target element.
    @ViewChild('container', { read: ElementRef }) container: ElementRef;
    // The Dialog shows within the target element.
    public targetElement: HTMLElement;
    // Sample level code to handle the button click action
    public onOpenDialog = function(event: any): void {
        // Call the show method to open the Dialog
        this.ejDialog.show();
    }
    ngOnInit() {
      // Load French culture for Dialog close button tooltip text
        L10n.load({
            'fr-BE': {
            'dialog': {
                    'close': "Fermer"
                }
            }
        });
        this.initilaizeTarget();
    }

    // Initialize the Dialog component target element.
    public initilaizeTarget: EmitType<object> = () => {
      this.targetElement = this.container.nativeElement.parentElement;
    }
}
```

{% endtab %}
