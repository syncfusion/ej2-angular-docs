# ColorPicker in DropDownButton

This section explains about how to render the ColorPicker in DropDownButton. The
[`target`](../../api/drop-down-button#target) property of the DropDownButton helps to achieve this scenario. To know about the usage of `target` property refer to [`Popup templating`](./../../drop-down-button/popup-items#popup-templating) section.

In the below sample, the color picker is rendered as inline type by setting [`inline`](../../api/color-picker#inline) property as `true` and the rendered color picker wrapper is passed as a `target` to the DropDownButton to achieve the above scenario.

{% tab template="colorpicker/dropdownbtn", sourceFiles="app/**/*.ts,index.css", isDefaultActive=true %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { DropDownButtonComponent } from '@syncfusion/ej2-angular-splitbuttons';
import { ColorPickerEventArgs } from '@syncfusion/ej2-angular-inputs';

@Component({
    selector: 'app-root',
    template: `<h4>Choose color</h4>
               <input ejs-colorpicker type="color" id="element" [inline]="true" (change)="change($event)" />
                <button ejs-dropdownbutton #dropdownbtn id="dropdownbtn" (open)="onOpen($event)" (beforeClose)="onClose($event)" target=".e-colorpicker-wrapper" iconCss="e-dropdownbtn-preview"></button>`
})

export class AppComponent {
    @ViewChild('dropdownbtn')
    private ddb: DropDownButtonComponent;

    public onOpen(args: any): void {
        args.element.parentElement.querySelector('.e-cancel').addEventListener('click', this.closePopup.bind(this));
    }

    public onClose(args: any): void {
        args.element.parentElement.querySelector('.e-cancel').removeEventListener('click', this.closePopup.bind(this));
    }

    public closePopup(): void {
        this.ddb.toggle();
    }

    // Triggers while selecting colors from color picker.
    public change(args: ColorPickerEventArgs): void {
        (this.ddb.element.children[0] as HTMLElement).style.backgroundColor = args.currentValue.hex;
        this.closePopup();
    }
 }
```

{% endtab %}
