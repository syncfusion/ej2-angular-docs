---
title: "Add floating label to read-only textbox"
component: "Textbox"
description: "Covers customization of the text box component such as a rounded corner, disabled, read-only state, background color, and font color."
---

# Add floating label to read-only TextBox

You can achieve floating label for read-only textboxes by adding/removing `e-label-top` and `e-label-bottom` classes to the label element

In this sample, click the update value button to fill the read-only textbox with value and float a label.

{% tab template="textbox/read-only", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<div class="wrap">
                <div class="row">
                  <div class="col-xs-6 col-sm-6 col-lg-6 col-md-6">
                      <div class="e-float-input">
                        <input class="e-input myField" id="myText" name="readonlyAttr"  type="text" readOnly>
                        <span class="e-float-line"></span>
                        <label class="e-float-text">Enter value</label>
                      </div>
                    </div>
                </div>
                <div class="row">
                  <div class="col-xs-10 col-sm-10 col-lg-10 col-md-10">
                      <button ejs-button class="e-btn update_value" id='valuebtn' >Set value</button>
                      <button ejs-button class="e-btn remove_value" id='removebtn' >Remove value</button>
                    </div>
                </div>
              </div>`
})

export class AppComponent {
  ngAfterViewInit(): void {
      document.getElementById('valuebtn').onclick = () => {
        (document.getElementsByClassName('myField')[0]).value = '10';
        checkFloatingLabel('myText')
      }
      document.getElementById('removebtn').addEventListener('click', function() {
        (document.getElementsByClassName('myField')[0]).value = '';
        checkFloatingLabel('myText')
      })
  }
  function checkFloatingLabel(id): void {
    let inputElement=  document.getElementById(id);
    let labelElement = inputElement.parentElement.querySelector('.e-float-text');
    if (inputElement.value !== '') {
        labelElement.classList.remove('e-label-bottom');
        labelElement.classList.add('e-label-top');
    } else {
      labelElement.classList.remove('e-label-top');
      labelElement.classList.add('e-label-bottom');
    }
  }
  let inputField = document.getElementById('myText');
}

```

{% endtab %}
