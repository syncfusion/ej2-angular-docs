---
title: "Migration from Essential JS 1"
component: "TimePicker"
description: "Explains the common steps for migrating from Essential JS 1 application to Essential JS 2 components especially, time picker component."
---

# Migration from Essential JS 1

This article describes the API migration process of TimePicker component from Essential JS 1 to Essential JS 2.

## Time Selection

<!-- markdownlint-disable MD033 -->
<table>
<thead>
<tr>
<th>Behavior</th>
<th>API in Essential JS 1</th>
<th>API in Essential JS 2</th>
</tr>
<tr>
<td>
Setting the value
</td>
<td>
<b>Property:</b> <i>value</i>

```html
<input type="text" ej-timepicker id="timePicker" value='5/5/2019 3:00 AM'/>
```

</td>
<td>
<b>Property:</b> <i>value</i>

```html
<ejs-timepicker id="timepicker" value='5/5/2019 3:00 AM'></ejs-timepicker>
```

</td>
</tr>
</thead>
</table>

## Time Format

<!-- markdownlint-disable MD033 -->
<table>
<thead>
<tr>
<th>Behavior</th>
<th>API in Essential JS 1</th>
<th>API in Essential JS 2</th>
</tr>
<tr>
<td>
Display time format
</td>
<td>
<b>Property:</b> <i>timeFormat</i>

```html
<input type="text" ej-timepicker id="timePicker" timeFormat='hh:mm:ss tt'/>
```

</td>
<td>
<b>Property:</b> <i>format</i>

```html
<ejs-timepicker id="timepicker"  format='hh:mm:ss'></ejs-timepicker>
```

</td>
</tr>
</thead>
</table>

## Time Range

<!-- markdownlint-disable MD033 -->
<table>
<thead>
<tr>
<th>Behavior</th>
<th>API in Essential JS 1</th>
<th>API in Essential JS 2</th>
</tr>
<tr>
<td>
Minimum time
</td>
<td>
<b>Property:</b> <i>minTime</i>

```html
<input type="text" ej-timepicker id="timePicker" minTime='10:00 AM'/>
```

</td>
<td>
<b>Property:</b> <i>min</i>

```html
<ejs-timepicker id='timepicker' min='5/5/2019 3:00 AM'></ejs-timepicker>
```

</td>
</tr>
<tr>
<td>
Maximum time
</td>
<td>
<b>Property:</b> <i>maxTime</i>

```html
<input type="text" ej-timepicker id="timePicker" maxTime='10:00 AM'/>
```

</td>
<td>
<b>Property:</b> <i>Max</i>

```html
<ejs-timepicker id='timepicker' max='5/5/2019 3:00 AM'></ejs-timepicker>
```

</td>
</tr>
<tr>
<td>
Set current time
</td>
<td>
<b>Method:</b> <i>setCurrentTime()</i>

```html
<input type="text" ej-timepicker id="timePicker" (create)="onCreate($event)"/>
```

```ts
public onCreate(e:any) {
    var timeObj = $("#timePicker").data("ejTimePicker");
    timeObj.setCurrentTime();
}
```

</td>
<td>
<b>Can be achieved by</b>

```ts
public value: Date = new Date();
```

```html
<ejs-timepicker id='timepicker' [value]='value'></ejs-timepicker>
```

</td>
</tr>
</thead>
</table>

## Disabled Time Ranges

<!-- markdownlint-disable MD033 -->
<table>
<thead>
<tr>
<th>Behavior</th>
<th>API in Essential JS 1</th>
<th>API in Essential JS 2</th>
</tr>
<tr>
<td>
Disable time ranges
</td>
<td>
<b>Property:</b> <i>disableTimeRanges</i>

```html
<input type="text" ej-timepicker id="timePicker" [disableTimeRanges]="disableTime"/>
```

```ts
disableTime: Object = [{ startTime: '3:00 AM', endTime: '6:00 AM' }, { startTime: '1:00 PM', endTime: '3:00 PM' }, { startTime: '8:00 PM', endTime: '10:00 PM' }];
```

</td>
<td>
<b>Can be achieved by</b>

```html
<ejs-timepicker id='timepicker' (itemRender)='itemRenderHandler($event)'></ejs-timepicker>
```

```ts
public itemRenderHandler(args: ItemEventArgs): void {
    if (args.value.getHours() === 4) {
        args.isDisabled = true;
    }
}
```

</td>
</tr>
</thead>
</table>

## Customization

<!-- markdownlint-disable MD033 -->
<table>
<thead>
<tr>
<th>Behavior</th>
<th>API in Essential JS 1</th>
<th>API in Essential JS 2</th>
</tr>
<tr>
<td>
CSS Class
</td>
<td>
<b>Property:</b> <i>CssClass</i>

```html
<input type="text" ej-timepicker id="timePicker" cssClass="gradient-lime"/>
```

</td>
<td>
<b>Property:</b> <i>CssClass</i>

```html
<ejs-timepicker id='timepicker' cssClass='e-custom-style'></ejs-timepicker>
```

</td>
</tr>
<tr>
<td>
Popup list customization
</td>
<td>
<b>Not Applicable</b>
</td>
<td>
<b>Event:</b> <i>itemRender</i>

```html
<ejs-timepicker id='timepicker' (itemRender)='itemRanderHandler($event)'></ejs-timepicker>
```

```ts
public itemRenderHandler(args: ItemEventArgs): void {/** code block */ }
```

</td>
</tr>
<tr>
<td>
Show/Hide the popup button
</td>
<td>
<b>Property:</b> <i>showPopupButton</i>

```html
<input type="text" ej-timepicker id="timePicker" [showPopupButton]="false"/>
```

</td>
<td>
<b>Can be achieved by</b>

```html
<ejs-timepicker id='timepicker' #timeObj (focus)='onFocus($event)'></ejs-timepicker>
```

```ts
@ViewChild("timeObj") timeObj: TimePickerComponent;

public onFocus(args:any):void {
    this.timeObj.show();
}
```

```css
.e-control-wrapper .e-input-group-icon.e-time-icon {
    display: none;
}
```

</td>
</tr>
<tr>
<td>
Enable/Disable the rounded corner
</td>
<td>
<b>Property:</b> <i>showRoundedCorner</i>

```html
<input type="text" ej-timepicker id="timePicker" [showRoundedCorner]="true"/>
```

</td>
<td>
<b>Can be achieved by</b>

```html
<ejs-timepicker id='timepicker' cssClass='e-custom-style'></ejs-timepicker>
```

```css
.e-control-wrapper.e-custom-style.e-time-wrapper.e-input-group {
    border-radius: 4px;
}
```

</td>
</tr>
<tr>
<td>
Enable/Disable the animation
</td>
<td>
<b>Property:</b> <i>enableAnimation</i>

```html
<input type="text" ej-timepicker id="timePicker" [enableAnimation]="true"/>
```

</td>
<td>
<b>Not Applicable</b>
</td>
</tr>
<tr>
<td>
Interval
</td>
<td>
<b>Property:</b> <i>interval</i>

```html
<input type="text" ej-timepicker id="timePicker" [interval]=120/>
```

</td>
<td>
<b>Property:</b> <i>step</i>

```html
<ejs-timepicker id='timepicker' step='120'></ejs-timepicker>
```

</td>
</tr>
<tr>
<td>
FocusIn event
</td>
<td>
<b>Event:</b> <i>focusIn</i>

```html
<input type="text" ej-timepicker id="timePicker" (focusIn)="onFocus($event)"/>
```

```ts
public onFocus(e:any) { /** code block */}
```

</td>
<td>
<b>Event:</b> <i>focus</i>

```html
<ejs-timepicker id='timepicker' #timeObj (focus)='onFocus($event)'></ejs-timepicker>
```

```ts
@ViewChild("timeObj") timeObj: TimePickerComponent;

public onFocus(args:any):void {
    /** code block */
}
```

</td>
</tr>
<tr>
<td>
FocusOut event
</td>
<td>
<b>Event:</b> <i>focusOut</i>

```html
<input type="text" ej-timepicker id="timePicker" (focusOut)="onFocus($event)"/>
```

```ts
public onFocus(e:any) { /** code block */}
```

</td>
<td>
<b>Event:</b> <i>blur</i>

```html
<ejs-timepicker id='timepicker' #timeObj  (blur)='onBlur($event)'></ejs-timepicker>
```

```ts
@ViewChild("timeObj") timeObj: TimePickerComponent;

public onBlur(args:any):void {
    /** code block */
}
```

</td>
</tr>
<tr>
<td>
FocusIn method
</td>
<td>
<b>Not Applicable</b>
</td>
<td>
<b>Method:</b> <i>focusIn()</i>

```html
<ejs-timepicker id='timepicker' #timeObj (created)='create($event)'></ejs-timepicker>
```

```ts
@ViewChild("timeObj") timeObj: TimePickerComponent;

public create(args:any):void {
    this.timeObj.focusIn();
}
```

</td>
</tr>
<tr>
<td>
FocusOut method
</td>
<td>
<b>Not Applicable</b>
</td>
<td>
<b>Event:</b> <i>focusOut</i>

```html
<ejs-timepicker id='timepicker' #timeObj (created)='create($event)'></ejs-timepicker>
```

```ts
@ViewChild("timeObj") timeObj: TimePickerComponent;

public create(args:any):void {
    this.timeObj.focusOut();
}
```

</td>
</tr>
<tr>
<td>
Prevent popup close
</td>
<td>
<b>Not Applicable</b>
</td>
<td>
<b>Event:</b> <i>close</i>

```html
<ejs-timepicker id='timepicker' #timeObj (close)='onClose($event)'></ejs-timepicker>
```

```ts
@ViewChild("timeObj") timeObj: TimePickerComponent;

public onClose(args:any): void {
     args.cancel = true;
}
```

</td>
</tr>
<tr>
<td>
Prevent popup open
</td>
<td>
<b>Not Applicable</b>
</td>
<td>
<b>Event:</b> <i>open</i>

```html
<ejs-timepicker id='timepicker' #timeObj (open)='onOpen($event)'></ejs-timepicker>
```

```ts
@ViewChild("timeObj") timeObj: TimePickerComponent;

public onOpen(args:any): void {
     args.cancel = true;
}
```

</td>
</tr>
</thead>
</table>

## Accessibility

<!-- markdownlint-disable MD033 -->
<table>
<thead>
<tr>
<th>Behavior</th>
<th>API in Essential JS 1</th>
<th>API in Essential JS 2</th>
</tr>
<tr>
<td>
Enable/Disable the RTL
</td>
<td>
<b>Property:</b> <i>enableRTL</i>

```html
<input type="text" ej-timepicker id="timePicker" [enableRTL]="true"/>
```

</td>
<td>
<b>Property:</b> <i>enableRtl</i>

```html
<ejs-timepicker id='timepicker' #timeObj enableRtl='true'></ejs-timepicker>
```

</td>
</tr>
</thead>
</table>

## Persistence

<!-- markdownlint-disable MD033 -->
<table>
<thead>
<tr>
<th>Behavior</th>
<th>API in Essential JS 1</th>
<th>API in Essential JS 2</th>
</tr>
<tr>
<td>
Enable/Disable the persistence
</td>
<td>
<b>Property:</b> <i>enablePersistence</i>

```html
<input type="text" ej-timepicker id="timePicker" [enablePersistence]="true"/>
```

</td>
<td>
<b>Property:</b> <i>enablePersistence</i>

```html
<ejs-timepicker id='timepicker' #timeObj enablePersistence='true'></ejs-timepicker>
```

</td>
</tr>
</thead>
</table>

## Validation

<!-- markdownlint-disable MD033 -->
<table>
<thead>
<tr>
<th>Behavior</th>
<th>API in Essential JS 1</th>
<th>API in Essential JS 2</th>
</tr>
<tr>
<td>
Validation rules
</td>
<td>
<b>Property:</b> <i>validationRules</i>

```html
<input type="text" ej-timepicker id="timePicker"  [validationRules]="validationRules"/>
```

```ts
validationRules:Object;
constructor(){
    this.validationRules = {required:true};
}
```

</td>
<td>
<b>Can be achieved by</b>

```html
<ejs-timepicker #timepicker id="timepicker" floatLabelType='Always'></ejs-timepicker>
```

```ts
let options: FormValidatorModel = {
    rules: {
        'timepicker': { required: [true, "Value is required"] } }};
        this.formObject = new FormValidator('#form-element', options);
```

</td>
</tr>
<tr>
<td>
Validation message
</td>
<td>
<b>Property:</b> <i>validationMessages</i>

```html
<input type="text" ej-timepicker id="timePicker"  [validationRules]="validationRules" [validationMessages]="validationMessages"/>
```

```ts
validationRules:Object;
validationMessages:Object;
constructor(){
    this.validationMessages = {required: "Required Time value"};
    this.validationRules = {required:true};
}
```

</td>
<td>
<b>Can be achieved by</b>

```html
<ejs-timepicker #timepicker id="timepicker" floatLabelType='Always'></ejs-timepicker>
```

```ts
let options: FormValidatorModel = {
    rules: {
        'timepicker': {
                    required: [true, "Value is required"]
                }
            },
            customPlacement: (inputElement: HTMLElement, errorElement: HTMLElement) => {
                inputElement.parentElement.parentElement.appendChild(errorElement);
            }
        };
this.formObject = new FormValidator('#form-element', options);
```

</td>
</tr>
</thead>
</table>

## Common

<!-- markdownlint-disable MD033 -->
<table>
<thead>
<tr>
<th>Behavior</th>
<th>API in Essential JS 1</th>
<th>API in Essential JS 2</th>
</tr>
<tr>
<td>
Width
</td>
<td>
<b>Property:</b> <i>width</i>

```html
<input type="text" ej-timepicker id="timePicker" width="300px"/>
```

</td>
<td>
<b>Property:</b> <i>width</i>

```html
<ejs-timepicker id='timepicker' width='200px'></ejs-timepicker>
```

</td>
</tr>
<tr>
<td>
Readonly
</td>
<td>
<b>Property:</b> <i>readOnly</i>

```html
<input type="text" ej-timepicker id="timePicker"  [readOnly]="true"/>
```

</td>
<td>
<b>Property:</b> <i>Readonly</i>

```html
<ejs-timepicker id='timepicker' readonly='true' value='5/5/2019 12:00 AM'></ejs-timepicker>
```

</td>
</tr>
<tr>
<td>
Show/Hide the clear button
</td>
<td>
<b>Not Applicable</b>
</td>
<td>
<b>Property:</b> <i>showClearButton</i>

```html
<ejs-timepicker id='timepicker' showClearButton='true'></ejs-timepicker>
```

</td>
</tr>
<tr>
<td>
Height
</td>
<td>
<b>Property:</b> <i>Height</i>

```html
<input type="text" ej-timepicker id="timePicker" height="50px"/>
```

</td>
<td>
<b>Can be achieved by</b>

```html
<ejs-timepicker id='timepicker' cssClass='e-custom-style'></ejs-timepicker>
```

```css
.e-control-wrapper.e-custom-style.e-time-wrapper.e-input-group {
    height: 35px;
}
```

</td>
</tr>
<tr>
<td>
Html Attributes
</td>
<td>
<b>Property:</b> <i>HtmlAttributes</i>

```html
<input type="text" ej-timepicker id="timePicker" [htmlAttributes]="htmlAttributes"/>
```

```ts
htmlAttributes: Object = {required:"required"}
```

</td>
<td>
<b>Not Applicable</b>
</td>
</tr>
<tr>
<td>
Watermark text
</td>
<td>
<b>Property:</b> <i>watermarkText</i>

```html
<input type="text" ej-timepicker id="timePicker" watermarkText="Enter Time"/>
```

</td>
<td>
<b>Property:</b> <i>placeholder</i>

```html
<ejs-timepicker id='timepicker' placeholder='Select a Time'></ejs-timepicker>
```

</td>
</tr>
<tr>
<td>
Enable the TimePicker
</td>
<td>
<b>Property:</b> <i>enabled</i>

```html
<input type="text" ej-timepicker id="timePicker" [enabled]="true"/>
```

</td>
<td>
<b>Property:</b> <i>enabled</i>

```html
<ejs-timepicker id='timepicker' enabled='true'></ejs-timepicker>
```

</td>
</tr>
<tr>
<td>
Disable the TimePicker
</td>
<td>
<b>Method:</b> <i>disable()</i>

```html
<input type="text" ej-timepicker id="timePicker" (create)="onCreate($event)"/>
```

```ts
public onCreate(e:any) {
    var timeObject = $("#timePicker").data("ejTimePicker");
    timeObject.disable();
}
```

</td>
<td>
<b>Property:</b> <i>enabled</i>

```html
<ejs-timepicker id='timepicker' enabled='false'></ejs-timepicker>
```

</td>
</tr>
<tr>
<td>
Enable/Disable the textBox editing
</td>
<td>
<b>Not Applicable</b>
</td>
<td>
<b>Property:</b> <i>allowEdit</i>

```html
<ejs-timepicker id='timepicker' allowEdit='false'></ejs-timepicker>
```

</td>
</tr>
<tr>
<td>
zIndex
</td>
<td>
<b>Not Applicable</b>
</td>
<td>
<b>Property:</b> <i>zIndex</i>

```html
<ejs-timepicker id='timepicker' zIndex='2000'></ejs-timepicker>
```

</td>
</tr>
<tr>
<td>
Specify the placeholder text behavior
</td>
<td>
<b>Not Applicable</b>
</td>
<td>
<b>Property:</b> <i>floatLabelType</i>

```html
<ejs-timepicker id='timepicker' floatLabelType='Always'></ejs-timepicker>
```

</td>
</tr>
</thead>
</table>

## Globalization

<!-- markdownlint-disable MD033 -->
<table>
<thead>
<tr>
<th>Behavior</th>
<th>API in Essential JS 1</th>
<th>API in Essential JS 2</th>
</tr>
<tr>
<td>
Locale
</td>
<td>
<b>Property:</b> <i>locale</i>

```html
<input type="text" ej-timepicker id="timePicker" locale="en-US"/>
```

</td>
<td>
<b>Property:</b> <i>locale</i>

```html
<ejs-timepicker id='timepicker' locale='en'></ejs-timepicker>
```

</td>
</tr>
</thead>
</table>

## Strict Mode

<!-- markdownlint-disable MD033 -->
<table>
<thead>
<tr>
<th>Behavior</th>
<th>API in Essential JS 1</th>
<th>API in Essential JS 2</th>
</tr>
<tr>
<td>
Strict mode
</td>
<td>
<b>Property:</b> <i>enableStrictMode</i>

```html
<input type="text" ej-timepicker id="timePicker" [enableStrictMode]="true"/>
```

</td>
<td>
<b>Property:</b> <i>strictMode</i>

```html
<ejs-timepicker id='timepicker' strictMode='true'></ejs-timepicker>
```

</td>
</tr>
</thead>
</table>

## Open and Close

<!-- markdownlint-disable MD033 -->
<table>
<thead>
<tr>
<th>Behavior</th>
<th>API in Essential JS 1</th>
<th>API in Essential JS 2</th>
</tr>
<tr>
<td>
Close
</td>
<td>
<b>Event:</b> <i>close</i>

```html
<input type="text" ej-timepicker id="timePicker" (close)="onClose($event)"/>
```

```ts
public onClose(e:any) {/** code block */ }
```

</td>
<td>
<b>Event:</b> <i>close</i>

```html
<ejs-timepicker id='timepicker' #timeObj (close)='onClose($event)'></ejs-timepicker>
```

```ts
@ViewChild("timeObj") timeObj: TimePickerComponent;

public onClose(args:any): void {/** code block */ }
```

</td>
</tr>
<tr>
<td>
Open
</td>
<td>
<b>Event:</b> <i>open</i>

```html
<input type="text" ej-timepicker id="timePicker" (open)="onOpen($event)"/>
```

```ts
public onOpen(e:any) {/** code block */ }
```

</td>
<td>
<b>Event:</b> <i>open</i>

```html
<ejs-timepicker id='timepicker' #timeObj (open)='onOpen($event)'></ejs-timepicker>
```

```ts
@ViewChild("timeObj") timeObj: TimePickerComponent;

public onOpen(args:any): void {/** code block */ }
```

</td>
</tr>
<tr>
<td>
Hide
</td>
<td>
<b>Method:</b> <i>hide()</i>

```html
<input type="text" ej-timepicker id="timePicker" (create)="onCreate($event)"/>
```

```ts
public onCreate(e:any) {
    var timeObject = $("#timePicker").data("ejTimePicker");
    timeObject.show();
    timeObject.hide();
}
```

</td>
<td>
<b>Method:</b> <i>hide()</i>

```html
<ejs-timepicker id='timepicker' #timeObj (created)='create($event)'></ejs-timepicker>
```

```ts
@ViewChild("timeObj") timeObj: TimePickerComponent;

public create(args:any): void {
    this.timeObj.show();
    this.timeObj.hide();
 }
```

</td>
</tr>
<tr>
<td>
Show
</td>
<td>
<b>Method:</b> <i>show()</i>

```html
<input type="text" ej-timepicker id="timePicker" (create)="onCreate($event)"/>
```

```ts
public onCreate(e:any) {
    var timeObject = $("#timePicker").data("ejTimePicker");
    timeObject.show();

}
```

</td>
<td>
<b>Method:</b> <i>show()</i>

```html
<ejs-timepicker id='timepicker' #timeObj (created)='create($event)'></ejs-timepicker>
```

```ts
@ViewChild("timeObj") timeObj: TimePickerComponent;

public create(args:any): void {
    this.timeObj.show();
}
```

</td>
</tr>
</thead>
</table>