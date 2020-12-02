# Customize ColorPicker

## Custom palette

By default, the Palette will be rendered with default colors. To load custom colors in the palette, specify the colors in the [`presetColors`](../../api/color-picker#presetcolors) property. To customize the color palette, add a custom class to palette tiles using [`BeforeTileRender`](../../api/color-picker#beforetilerender) event.

The following sample demonstrates the above functionalities.

{% tab template="colorpicker/custom/palette", sourceFiles="app/**/*.ts,index.css", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { PaletteTileEventArgs, ColorPickerEventArgs } from '@syncfusion/ej2-inputs';
import { addClass } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    template: `<div id="preview"></div>
               <h4>Select Color</h4>
               <input ejs-colorpicker type="color" id="element" value="#ba68c8" mode="Palette" [columns]="colCount" [inline]="true" [modeSwitcher]="false" [showButtons]="false" [presetColors]="customColors" (beforeTileRender)="tileRender($event)" (change)="onChange($event)" />`
})

export class AppComponent {
        public tileRender(args: PaletteTileEventArgs): void {
            addClass([args.element], ['e-icons', 'e-custom-tile']);
        }

        // To specify number of columns to be rendered.
        public colCount: number = 4;

        // Triggers while selecting colors from palette.
        public onChange(args: ColorPickerEventArgs): void {
            document.getElementById('preview').style.backgroundColor = args.currentValue.hex;
        }

        // Triggers before rendering each palette tile.
        public customColors: { [key: string]: string[] } = {
                'custom1': ['#ef9a9a', '#e57373', '#ef5350',
                        '#f44336', '#f48fb1', '#f06292',
                        '#ec407a', '#e91e63', '#ce93d8',
                        '#ba68c8', '#ab47bc', '#9c27b0',
                        '#b39ddb', '#9575cd', '#7e57c2', '#673AB7'],
                'custom2': ['#9FA8DA', '#7986CB', '#5C6BC0', '#3F51B5',
                        '#90CAF9', '#64B5F6', '#42A5F5', '#2196F3',
                        '#81D4FA', '#4FC3F7', '#29B6F6', '#03A9F4',
                        '#80DEEA', '#4DD0E1', '#26C6DA', '#00BCD4'],
                'custom3': ['#80CBC4', '#4DB6AC', '#26A69A', '#009688',
                        '#A5D6A7', '#81C784', '#66BB6A', '#4CAF50',
                        '#C5E1A5', '#AED581', '#9CCC65', '#8BC34A', '#E6EE9C',
                        '#DCE775', '#D4E157', '#CDDC39']
        };

        ngOnInit(): void {
            (document.getElementById('preview') as HTMLElement).style.backgroundColor = "#ba68c8"
        }
 }
```

{% endtab %}

## Hide input area from picker

By default, the input area will be rendered in ColorPicker. To hide the input area from it, add `e-hide-value` class to ColorPicker using the [`cssClass`](../../api/color-picker#cssclass) property.

In the following sample, the ColorPicker is rendered without input area.

{% tab template="colorpicker/how-to", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<h4>Choose Color</h4>
               <!-- To hide the value area. -->
               <input ejs-colorpicker type="color" id="element" cssClass="e-hide-value" [modeSwitcher]="false" />`
})

export class AppComponent { }
```

{% endtab %}

## Custom handle

Color picker handle shape and UI can be customized. Here, we have customized the handle as `svg icon`. The same way you can customize the handle based on your requirement.

The following sample show the customized color picker handle.

{% tab template="colorpicker/custom/handle", sourceFiles="app/**/*.ts,index.css", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { OpenEventArgs } from '@syncfusion/ej2-angular-inputs';

@Component({
    selector: 'app-root',
    template: `<h4>Choose Color</h4>
               <!-- custom picker -->
               <input ejs-colorpicker type="color" id="element" value="#344aae" cssClass="e-custom-picker" [modeSwitcher]="false" (open)="onOpen($event)" />`
})

export class AppComponent {
    onOpen(args: OpenEventArgs): void {
        args.element.querySelector('.e-handler').classList.add('e-icons');
    }
}
```

{% endtab %}

## Custom primary button

By default, the applied color will be updated in primary button of the color picker. You can customize that as `icon`.

In the following sample, the `picker` icon is added to primary button and using [`change`](../../api/color-picker#change) event the selected color will be updated in bottom portion of the icon.

{% tab template="colorpicker/icon", sourceFiles="app/**/*.ts,index.html,index.css", isDefaultActive=true %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { addClass } from '@syncfusion/ej2-base';
import { ColorPickerEventArgs, ColorPickerComponent } from '@syncfusion/ej2-angular-inputs';

@Component({
    selector: 'app-root',
    template: `<h4>Choose color</h4>
               <input ejs-colorpicker #colorpicker id="element" (change)="onChange($event)" />`
})

export class AppComponent {
    @ViewChild('colorpicker')
    private colorPicker: ColorPickerComponent;

    public onChange(args: ColorPickerEventArgs): void {
        (this.colorPicker.element.nextElementSibling.querySelector('.e-selected-color') as HTMLElement).style.borderBottomColor = args.currentValue.rgba;
    }

    ngOnInit(): void {
        setTimeout(() => {
            addClass([this.colorPicker.element.nextElementSibling.querySelector('.e-selected-color')], 'e-icons');
        }, 500);
    }
 }
```

{% endtab %}

>> The Essential JS 2 provides a set of icons that can be loaded by applying `e-icons` class name to the element. You can also use third party icon to customize the primary button.

## Display hex code in input

The color picker input element can be showcased in the place of primary button. The applied color hex code will be updated in the primary button input.

The following sample shows the color picker with input.

{% tab template="colorpicker/input", sourceFiles="app/**/*.ts,index.css", isDefaultActive=true %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { ColorPickerComponent } from '@syncfusion/ej2-angular-inputs';

@Component({
    selector: 'app-root',
    template: `<h4>Choose color</h4>
               <input ejs-colorpicker #colorpicker id="element" readonly />`
})

export class AppComponent {
    @ViewChild('colorpicker')
    public colorPicker: ColorPickerComponent;

    ngOnInit(): void {
        this.colorPicker.element.type = 'text';
        this.colorPicker.element.classList.add('e-input');
        setTimeout(() => {
            let proxy: any = this;
            let target: HTMLElement = proxy.colorPicker.element.nextElementSibling;
            target.insertBefore(proxy.colorPicker.element, target.children[1]);
        }, 500);
    }
 }
```

{% endtab %}

## Custom UI

The color picker UI can be customized in all possible ways. The following sample shows the excel like UI customization with help of SplitButton and Dialog component. In that by clicking the more colors option from color palette, the dialog contains color picker will open.

{% tab template="colorpicker/position", sourceFiles="app/**/*.ts,index.css", isDefaultActive=true %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { ColorPickerEventArgs } from '@syncfusion/ej2-inputs';
import { EmitType, formatUnit } from '@syncfusion/ej2-base';
import { ItemModel, MenuEventArgs, BeforeOpenCloseMenuEventArgs } from '@syncfusion/ej2-splitbuttons';
import { ColorPickerComponent } from '@syncfusion/ej2-angular-inputs';
import { DialogComponent } from '@syncfusion/ej2-angular-popups';
import { SplitButtonComponent } from '@syncfusion/ej2-angular-splitbuttons';

@Component({
    selector: 'app-root',
    template: `<h4>Select Color</h4>
                <input ejs-colorpicker #colorpalette type="color" id="colorpalette" cssClass="e-hide-palette" mode="Palette" [inline]="true" [showButtons]="false" [modeSwitcher]="false" (change)="paletteOnChange($event)" />
                <ejs-splitbutton #splitbutton iconCss="e-icons e-font-icon" [items]="items" (beforeClose)="onBeforeClose($event)" (beforeItemRender)="beforeRender($event)" (select)="onSelect($event)"></ejs-splitbutton>
                <ejs-dialog id="modalDialog" #modalDialog cssClass="e-dlg-picker" (open)="modalDlgOpen()" [isModal]="true" [width]="width" [height]="height" [visible]="false" [target]='target' [animationSettings]='animationSettings'
                (overlayClick)="dlgClose()">
                    <ng-template #content>
                        <input ejs-colorpicker #colorpicker type="color" id="colorpicker" (change)="pickerOnChange($event)" [inline]="true" [modeSwitcher]="false" />
                    </ng-template>
                </ejs-dialog>`
})
export class AppComponent {
    @ViewChild('colorpalette')
    public colorPalette: ColorPickerComponent;
    @ViewChild('colorpicker')
    public colorPicker: ColorPickerComponent;
    @ViewChild('modalDialog')
    public modalDialog: DialogComponent;
    @ViewChild('splitbutton')
    public splitBtn: SplitButtonComponent;

    public items: ItemModel[] = [
        {
            text: ''
        },
        {
            text: "More Colors...",
            iconCss: "e-switcher"
        }
    ];

    public target: string = ".wrap";
    public width: string = '270px';
    public height: string = '336px';
    public animationSettings: Object = { effect: 'Zoom' };

    public beforeRender(args: MenuEventArgs): void {
        if (args.item.text === "") {
            this.colorPalette.cssClass = "";
            this.colorPalette.dataBind();
            this.colorPalette.refresh();
            args.element.appendChild(this.colorPalette.element.parentElement);
        }
    }

    public modalDlgOpen: EmitType<object> = () => {
        this.colorPicker.refresh();
        (this.colorPicker.element.parentElement as HTMLElement).querySelector('.e-ctrl-btn .e-cancel').addEventListener('click', this.dlgClose);
    }

    public onBeforeClose(args: BeforeOpenCloseMenuEventArgs): void {
        document.body.appendChild(this.colorPalette.element.parentElement);
        this.colorPalette.cssClass = "e-hide-palette";
        this.colorPalette.dataBind();
    }

    public dlgClose: any = (args: any) => {
        this.modalDialog.hide();
    }

    public pickerOnChange(args: ColorPickerEventArgs): void {
        this.paletteOnChange(args);
        this.modalDialog.hide();
    }

    public paletteOnChange(args: ColorPickerEventArgs): void {
        (this.splitBtn.element.querySelector(".e-font-icon") as HTMLElement).style.borderBottomColor = args.currentValue.rgba;
    }

    public onSelect(args: MenuEventArgs): void {
        if (args.item.text === 'More Colors...') {
            this.modalDialog.show();
        }
    }
}
```

{% endtab %}