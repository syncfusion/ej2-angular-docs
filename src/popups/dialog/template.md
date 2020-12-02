---
title: "Angular Dialog Template"
component: "Dialog"
description: "Explains how to customize the dialog's user interface (UI) elements such as header, footer, and content using a template."
---

# Template Support

In Dialog the template support is provided to the header, content and footer sections. So any text or HTML content can be appending in these sections.

## Header

The Dialog header content can be provided through the
[`header`](../api/dialog/#header) property, and it will allow both text and any HTML content as a string.
Also in header, close button is provided as built-in support, and this can be enabled through
the [`showCloseIcon`](../api/dialog/#showcloseicon) property.

## Footer

The Dialog footer can be enabled by adding built-in [`buttons`](../api/dialog/#buttons) or providing any HTML string through the [`footerTemplate`](../api/dialog/#footertemplate).

> The `buttons` and [`footerTemplate`](../api/dialog/#footertemplate) properties can't be used at the same time.

The below example demonstrates the usage of header and footer template in the Dialog

## Content

The Dialog content can be update by providing any HTML string through the [`content`](../api/dialog/#content).

The below example demonstrates the usage of content as template in the Dialog

{% tab template="dialog/template", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript

import { Component, ViewChild, OnInit, ElementRef } from '@angular/core';
import { DialogComponent } from '@syncfusion/ej2-angular-popups';
import { EmitType, isNullOrUndefined } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    template: `
    <button class="e-control e-btn" style="position: absolute;" id="targetButton" (click)="onOpenDialog($event)">Open Dialog</button>
      <div #container class='root-container'></div>
      <ejs-dialog id='dialog' #template showCloseIcon='true' (open)="dialogOpen()" [height]='height' [target]='targetElement' width='435px'>
      <ng-template #footerTemplate>
            <input id="inVal" class="e-input" type="text" placeholder="Enter your message here!"/>
            <button id="sendButton" class="e-control e-btn e-primary sendButton" data-ripple="true">Send</button>
        </ng-template>
        <ng-template #content>
            <div class="dialogContent">
                <span class="dialogText">Greetings Nancy! When will you share me the source files of the project?</span>
            </div>
        </ng-template>
        <ng-template #header>
            <img class="img2" src="https://ej2.syncfusion.com/products/typescript/dialog/template/images/1.png" style="display: inline-block;" alt="header image"/>
            <div title="Nancy" class="e-icon-settings dlg-template"> Nancy </div>
        </ng-template>
      </ejs-dialog>
        `
})

export class AppComponent implements OnInit {
    @ViewChild('template') template: DialogComponent;
    // Create element reference for dialog target element.
    @ViewChild('container', { read: ElementRef }) container: ElementRef;
    // The Dialog shows within the target element.
    public targetElement: HTMLElement;
    public proxy: any = this;

    //To get all element of the dialog component after component get initialized.
    ngOnInit() {
      this.initilaizeTarget();
    }

    // Initialize the Dialog component target element.
    public initilaizeTarget: EmitType<object> = () => {
      this.targetElement = this.container.nativeElement.parentElement;
    }
    public height: string = '250px';
    public dialogOpen: EmitType<object> = () => {
        (document.getElementById('sendButton') as any).keypress = (e: any) => {
            if (e.keyCode === 13) { this.updateTextValue(); }
        };
        (document.getElementById('inVal')as HTMLElement).onkeydown = (e: any) => {
            if (e.keyCode === 13) { this.updateTextValue(); }
        };
        document.getElementById('sendButton').onclick = (): void => {
            this.updateTextValue();
        };
    }

    public updateTextValue: EmitType<object> = () => {
        let enteredVal: HTMLInputElement = document.getElementById('inVal') as HTMLInputElement;
        let dialogTextElement: HTMLElement = document.getElementsByClassName('dialogText')[0] as HTMLElement;
        let dialogTextWrap : HTMLElement = document.getElementsByClassName('dialogContent')[0] as HTMLElement;
        if (!isNullOrUndefined(document.getElementsByClassName('contentText')[0])) {
            detach(document.getElementsByClassName('contentText')[0]);
        }
        if (enteredVal.value !== '') {
            dialogTextElement.innerHTML = enteredVal.value;
        }
        enteredVal.value = '';
    }

    // Sample level code to handle the button click action
    public onOpenDialog = function(event: any): void {
        // Call the show method to open the Dialog
        this.template.show();
    }
}

```

{% endtab %}

## See Also

* [How to add an icon to dialog buttons](./how-to/add-an-icons-to-dialog-buttons)
* [How to customize the dialog appearance](./how-to/customize-the-dialog-appearance)
