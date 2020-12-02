---
title: "Repeat Button"
component: "Button"
description: "Angular Button how to section, block button, repeat button, tooltip for Button, customization of button appearance, input and anchor elements."
---

# Repeat Button

The repeat button is a type of button in that the click event is triggered at regular time
interval from the pressed state till the released state.

The following example explains about how to achieve repeat button in mouse and touch events.

{% tab template="button/repeat-button", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { ButtonComponent } from '@syncfusion/ej2-angular-buttons';

@Component({
    selector: 'app-root',
    template:  `<div id='container'>
                    <div class='btncontainer'>
                        <button #btn ejs-button (mousedown)="mousedown()" (mouseup)="mouseup()" (touchstart)="touchstart()" (touchend)="touchend()" (click)="onclick()">Button</button>
                    </div>
                    <div class='event' style="height:auto;">
                        <table title='Event Trace' style="width:100%">
                            <tbody>
                                <tr>
                                    <th>Event Trace</th>
                                </tr>
                                <tr>
                                    <td>
                                        <div class="eventarea" style="height: 250px;overflow: auto">
                                            <span id="eventlog" style="word-break: normal;"></span>
                                        </div>
                                    </td>
                                </tr>
                                <tr>
                                    <td>
                                        <div class="evtbtn" style="padding:20px 0 0 20px">
                                            <button #clear (click)="clearEvt()" ejs-button>Clear</button>
                                        </div>
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>`
})

export class AppComponent {
  @ViewChild('btn')
  private btn: ButtonComponent;
  @ViewChild('clear')
  private clear: ButtonComponent;
  private timeout: any;
  private spanElem: HTMLElement;
  private log: HTMLElement;
  
  mousedown() {
    this.timeout = setInterval(() => {
      this.spanElem = document.createElement('span');
      this.spanElem.innerHTML = 'Button click event triggered.<hr>';
      this.log = document.getElementById('eventlog');
      this.log.insertBefore(this.spanElem, this.log.firstChild);
    }, 200);
  };

  mouseup() {
    clearInterval(this.timeout);
  };

  touchstart() {
    this.timeout = setInterval(() => {
      this.spanElem = document.createElement('span');
      this.spanElem.innerHTML = 'Button click event triggered.<hr>';
      this.log = document.getElementById('eventlog');
      this.log.insertBefore(this.spanElem, this.log.firstChild);
    }, 200);
  };

  touchend() {
    clearInterval(this.timeout);
  };

  onclick() {
    this.spanElem = document.createElement('span');
    this.spanElem.innerHTML = 'Button click event triggered.<hr>';
    this.log = document.getElementById('eventlog');
    this.log.insertBefore(this.spanElem, this.log.firstChild);
  };

  clearEvt() {
    document.getElementById('eventlog').innerHTML = '';
  };
}

```

{% endtab %}