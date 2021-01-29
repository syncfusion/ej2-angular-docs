---
title: "Editor Window and Quick Popup of Scheduler"
component: "Scheduler"
description: "This topic demonstrates how to customize the default event editor and quick pop-up using templates and also explains how to design the custom modal popup."
---

# Editor window and quick popups

Scheduler makes use of popups and dialog to display the required notifications, as well as includes an editor window with event fields for making the appointment creation and editing process easier. You can also easily customize the editor window and the fields present in it, and can also apply validations on those fields.

## Event editor

The editor window usually opens on the Scheduler, when a cell or event is double clicked. When a cell is double clicked, the detailed editor window opens in "Add new" mode, whereas when an event is double clicked, the same is opened in an "Edit" mode.

In mobile devices, you can open the detailed editor window in edit mode by clicking the edit icon on the popup, that opens on single tapping an event. You can also open it in add mode by single tapping a cell, which will display a `+` indication, clicking on it again will open the editor window.

> You can also prevent the editor window from opening, by rendering Scheduler in a `readonly` mode or by doing code customization within the `popupOpen` event.

### How to change the editor window header title and text of footer buttons

You can change the header title and the text of buttons displayed at the footer of the editor window by changing the appropriate localized word collection used in the Scheduler.

{% tab template="schedule/editor-window", iframeHeight="588px", sourceFiles="app/**/*.ts" %}

```typescript
import { L10n } from '@syncfusion/ej2-base';
import { Component } from '@angular/core';
import { EventSettingsModel, DayService, WeekService, TimelineViewsService, MonthService, AgendaService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData} from './datasource.ts';

L10n.load({
  'en-US': {
      'schedule': {
          'saveButton': 'Add',
          'cancelButton': 'Close',
          'deleteButton': 'Remove',
          'newEvent': 'Add Event',
      },
  }
});
@Component({
  selector: 'app-root',
  providers: [DayService, WeekService, TimelineViewsService, MonthService, AgendaService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [selectedDate]='selectedDate' [views]='views' [eventSettings]='eventSettings'></ejs-schedule>`
})


export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public views: Array<string> = ['TimelineDay', 'Day', 'Week', 'Month', 'Agenda'];
    public eventSettings: EventSettingsModel = {
        dataSource: scheduleData
    };
 }
```

{% endtab %}

### How to change the label text of default editor fields

To change the default labels such as Subject, Location and other field names in the editor window, make use of the `title` property available within the field option of `eventSettings`.

{% tab template="schedule/editor-window", iframeHeight="588px", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, DayService, WeekService, TimelineViewsService, MonthService, AgendaService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData} from './datasource.ts';
@Component({
  selector: 'app-root',
  providers: [DayService, WeekService, TimelineViewsService, MonthService, AgendaService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [selectedDate]='selectedDate' [views]='views' [eventSettings]='eventSettings'></ejs-schedule>`
})


export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public views: Array<string> = ['Day', 'Week', 'TimelineWeek', 'Month', 'Agenda'];
    public eventSettings: EventSettingsModel = {
        dataSource: scheduleData,
        fields: {
            id: 'Id',
            subject: { name: 'Subject', title: 'Event Name' },
            location: { name: 'Location', title: 'Event Location'},
            description: { name: 'Description', title: 'Event Description' },
            startTime: { name: 'StartTime', title: 'Start Duration' },
            endTime: { name: 'EndTime', title: 'End Duration'  }
        }
    };
 }
```

{% endtab %}

### Field validation

It is possible to validate the required fields of the editor window from client-side before submitting it, by adding appropriate validation rules to each field. The appointment fields have been extended to accept both `string` and `object` type values. To perform validations, it is necessary to specify object values for the event fields.

{% tab template="schedule/editor-window", iframeHeight="588px", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, DayService, WeekService, WorkWeekService, MonthService, AgendaService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData} from './datasource.ts';
@Component({
  selector: 'app-root',
  providers: [DayService, WeekService, WorkWeekService, MonthService, AgendaService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [selectedDate]='selectedDate' [views]='views' [eventSettings]='eventSettings'></ejs-schedule>`
})


export class AppComponent {
    minValidation: (args: { [key: string]: string }) => boolean = (args: { [key: string]: string }) => {
        return args['value'].length >= 5;
    };
    public selectedDate: Date = new Date(2018, 1, 15);
    public views: Array<string> = ['Day', 'Week', 'WorkWeek', 'Month', 'Agenda'];
    public eventSettings: EventSettingsModel = {
        dataSource: scheduleData,
        fields: {
            id: 'Id',
            subject: { name: 'Subject', validation: { required: true } },
            location: { name: 'Location', validation: { required: true } },
            description: {
                name: 'Description', validation: {
                    required: true, minLength: [this.minValidation, 'Need atleast 5 letters to be entered']
                }
            },
            startTime: { name: 'StartTime', validation: { required: true } },
            endTime: { name: 'EndTime', validation: { required: true } }
        }
    };
 }
```

{% endtab %}

> Applicable validation rules can be referred from [form validation](http://ej2.syncfusion.com/documentation/form-validator/#validation-rules) documentation.

### Add additional fields to the default editor

The additional fields can be added to the default event editor by making use of the `popupOpen` event which gets triggered before the event editor opens on the Scheduler. The `popupOpen` is a client-side event that triggers before any of the generic popups opens on the Scheduler. The additional field (any of the form elements) should be added with a common class name `e-field`, so as to handle and process those additional data along with the default event object. In the following example, an additional field `Event Type` has been added to the default event editor and its value is processed accordingly.

{% tab template="schedule/editor-window", iframeHeight="588px", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { DropDownList } from '@syncfusion/ej2-dropdowns';
import { createElement } from '@syncfusion/ej2-base';
import { EventSettingsModel, DayService, WeekService, WorkWeekService, MonthService, PopupOpenEventArgs } from '@syncfusion/ej2-angular-schedule';
import { eventsData} from './datasource.ts';
@Component({
  selector: 'app-root',
  providers: [DayService, WeekService, WorkWeekService, MonthService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [selectedDate]='selectedDate' [views]='views' [eventSettings]='eventSettings' (popupOpen)='onPopupOpen($event)'></ejs-schedule>`
})


export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public views: Array<string> = ['Day', 'Week', 'WorkWeek', 'Month'];
    public eventSettings: EventSettingsModel = {
        dataSource: eventsData
    };
    onPopupOpen(args: PopupOpenEventArgs): void {
        if (args.type === 'Editor') {
            // Create required custom elements in initial time
            if (!args.element.querySelector('.custom-field-row')) {
                let row: HTMLElement = createElement('div', { className: 'custom-field-row' });
                let formElement: HTMLElement = args.element.querySelector('.e-schedule-form');
                formElement.firstChild.insertBefore(row, args.element.querySelector('.e-title-location-row'));
                let container: HTMLElement = createElement('div', { className: 'custom-field-container' });
                let inputEle: HTMLInputElement = createElement('input', {
                    className: 'e-field', attrs: { name: 'EventType' }
                }) as HTMLInputElement;
                container.appendChild(inputEle);
                row.appendChild(container);
                let dropDownList: DropDownList = new DropDownList({
                    dataSource: [
                        { text: 'Public Event', value: 'public-event' },
                        { text: 'Maintenance', value: 'maintenance' },
                        { text: 'Commercial Event', value: 'commercial-event' },
                        { text: 'Family Event', value: 'family-event' }
                    ],
                    fields: { text: 'text', value: 'value' },
                    value: (<{ [key: string]: Object }>(args.data)).EventType as string,
                    floatLabelType: 'Always', placeholder: 'Event Type'
                });
                dropDownList.appendTo(inputEle);
                inputEle.setAttribute('name', 'EventType');
            }
        }
    }
 }
```

{% endtab %}

### How to prevent the default focus of the editor widow

When we open the editor window, by default it will be focus to the `Subject` field. And we can able to prevent the default focusing of the editor window using the `popupOpen` event as shown in the following code example.

{% tab template="schedule/editor-window", iframeHeight="588px", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { EventSettingsModel, DayService, WeekService, WorkWeekService, MonthService, PopupOpenEventArgs, ScheduleComponent } from '@syncfusion/ej2-angular-schedule';
import { eventsData} from './datasource.ts';
@Component({
  selector: 'app-root',
  providers: [DayService, WeekService, WorkWeekService, MonthService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule #scheduleObj width='100%' height='550px' [selectedDate]='selectedDate' [views]='views' [eventSettings]='eventSettings' (popupOpen)='onPopupOpen($event)'></ejs-schedule>`
})


export class AppComponent {
    @ViewChild("scheduleObj")
    public scheduleObj: ScheduleComponent;
    public selectedDate: Date = new Date(2018, 1, 15);
    public views: Array<string> = ['Day', 'Week', 'WorkWeek', 'Month'];
    public eventSettings: EventSettingsModel = {
        dataSource: eventsData
    };
    onPopupOpen(args: PopupOpenEventArgs): void {
        if (args.type === 'Editor') {
            let dialog = args.element.ej2_instances[0];
            dialog.open = function(args) {
                this.scheduleObj.eventBase.focusElement();
            };
        }
    }
 }
```

{% endtab %}

### Customizing the default time duration in editor window

In default event editor window, start and end time duration are processed based on the `interval` value set within the `timeScale` property. By default, `interval` value is set to 30, and therefore the start/end time duration within the event editor will be in a 30 minutes time difference. You can change this duration value by changing the `duration` option within the `popupOpen` event as shown in the following code example.

{% tab template="schedule/editor-window", iframeHeight="588px", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, DayService, WeekService, WorkWeekService, MonthService, PopupOpenEventArgs } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource.ts';
@Component({
    selector: 'app-root',
    providers: [DayService, WeekService, WorkWeekService, MonthService],
    // specifies the template string for the Schedule component
    template: `<ejs-schedule width='100%' height='550px' [selectedDate]='selectedDate' [views]='views' [eventSettings]='eventSettings' (popupOpen)='onPopupOpen($event)'></ejs-schedule>`
})


export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public views: Array<string> = ['Day', 'Week', 'WorkWeek', 'Month'];
    public eventSettings: EventSettingsModel = {
        dataSource: scheduleData
    };
    onPopupOpen(args: PopupOpenEventArgs): void {
        if (args.type === 'Editor') {
            args.duration = 60;
        }
    }
}
```

{% endtab %}

### How to prevent the display of editor and quick popups

It is possible to prevent the display of editor and quick popup windows by passing the value `true` to `cancel` option within the `popupOpen` event.

{% tab template="schedule/editor-window", iframeHeight="588px", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, DayService, WeekService, WorkWeekService, MonthService, PopupOpenEventArgs } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource.ts';
@Component({
    selector: 'app-root',
    providers: [DayService, WeekService, WorkWeekService, MonthService],
    // specifies the template string for the Schedule component
    template: `<ejs-schedule width='100%' height='550px' [selectedDate]='selectedDate' [views]='views' [eventSettings]='eventSettings' (popupOpen)='onPopupOpen($event)'></ejs-schedule>`
})


export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public views: Array<string> = ['Day', 'Week', 'WorkWeek', 'Month'];
    public eventSettings: EventSettingsModel = {
        dataSource: scheduleData
    };
    onPopupOpen(args: PopupOpenEventArgs): void {
        if (args.type === 'Editor' || args.type === 'QuickInfo')  {
            args.cancel = true;
        }
    }
}
```

{% endtab %}

In case, if you need to prevent only specific popups on Scheduler, then you can check the condition based on the popup type. The types of the popup that can be checked within the `popupOpen` event are as follows.

| Type | Description |
|------|-------------|
| Editor | For Detailed editor window.|
| QuickInfo | For Quick popup which opens on cell click.|
| EditEventInfo |For  Quick popup which opens on event click.|
| ViewEventInfo | For Quick popup which opens on responsive mode.|
| EventContainer | For more event indicator popup.|
| RecurrenceAlert | For edit recurrence event alert popup.|
| DeleteAlert | For delete confirmation popup.|
| ValidationAlert | For validation alert popup.|
| RecurrenceValidationAlert | For recurrence validation alert popup.|

## Customizing event editor using template

The event editor window can be customized by making use of the `editorTemplate` option. Here, the custom window design is built with the required fields using the script template and its type should be of **text/x-template**.

Each field defined within template should contain the **e-field** class, so as to allow the processing of those field values internally. The ID of this customized script template section is assigned to the `editorTemplate` option, so that these customized fields will be replaced onto the default editor window.

As we are using our Syncfusion sub-components within our editor using template in the following example, the custom defined form elements needs to be configured as required Syncfusion components such as **DropDownList** and **DateTimePicker** within the `popupOpen` event. This particular step can be skipped, if the user needs to simply use the usual form elements.

Learn the easiest way to customize the editor window of Angular Scheduler with your own design by watching this video:

`youtube:-KJg2d6mdmQ`

{% tab template="schedule/editor-window", iframeHeight="588px", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { DropDownList } from '@syncfusion/ej2-dropdowns';
import { DateTimePicker } from '@syncfusion/ej2-calendars';
import { EventSettingsModel, DayService, WeekService, WorkWeekService, MonthService, PopupOpenEventArgs } from '@syncfusion/ej2-angular-schedule';
import { eventData } from './datasource.ts';
@Component({
    selector: 'app-root',
    providers: [DayService, WeekService, WorkWeekService, MonthService],
    // specifies the template string for the Schedule component
    template: `<ejs-schedule width='100%' height='550px' [selectedDate]='selectedDate' [views]='views' [eventSettings]='eventSettings' [showQuickInfo]='showQuickInfo' (popupOpen)='onPopupOpen($event)'>
    <ng-template #editorTemplate>
        <table class="custom-event-editor" width="100%" cellpadding="5">
            <tbody>
                <tr>
                    <td class="e-textlabel">Summary</td>
                    <td colspan="4">
                        <input id="Subject" class="e-field e-input" type="text" value="" name="Subject" style="width: 100%" />
                    </td>
                </tr>
                <tr>
                    <td class="e-textlabel">Status</td>
                    <td colspan="4">
                        <input type="text" id="EventType" name="EventType" class="e-field" style="width: 100%" />
                    </td>
                </tr>
                <tr>
                    <td class="e-textlabel">From</td>
                    <td colspan="4">
                        <input id="StartTime" class="e-field" type="text" name="StartTime" />
                    </td>
                </tr>
                <tr>
                    <td class="e-textlabel">To</td>
                    <td colspan="4">
                        <input id="EndTime" class="e-field" type="text" name="EndTime" />
                    </td>
                </tr>
                <tr>
                    <td class="e-textlabel">Reason</td>
                    <td colspan="4">
                        <textarea id="Description" class="e-field e-input" name="Description" rows="3" cols="50" style="width: 100%; height: 60px !important; resize: vertical"></textarea>
                    </td>
                </tr>
            </tbody>
        </table>
    </ng-template>
    </ejs-schedule>`
})


export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public views: Array<string> = ['Day', 'Week', 'WorkWeek', 'Month'];
    public showQuickInfo: Boolean = false;
    public eventSettings: EventSettingsModel = {
        dataSource: eventData
    };
    onPopupOpen(args: PopupOpenEventArgs): void {
        if (args.type === 'Editor') {
            let statusElement: HTMLInputElement = args.element.querySelector('#EventType') as HTMLInputElement;
            if (!statusElement.classList.contains('e-dropdownlist')) {
                let dropDownListObject: DropDownList = new DropDownList({
                    placeholder: 'Choose status', value: statusElement.value,
                    dataSource: ['New', 'Requested', 'Confirmed']
                });
                dropDownListObject.appendTo(statusElement);
                statusElement.setAttribute('name', 'EventType');
            }
            let startElement: HTMLInputElement = args.element.querySelector('#StartTime') as HTMLInputElement;
            if (!startElement.classList.contains('e-datetimepicker')) {
                new DateTimePicker({ value: new Date(startElement.value) || new Date() }, startElement);
            }
            let endElement: HTMLInputElement = args.element.querySelector('#EndTime') as HTMLInputElement;
            if (!endElement.classList.contains('e-datetimepicker')) {
                new DateTimePicker({ value: new Date(endElement.value) || new Date() }, endElement);
            }
        }
    }
}
```

{% endtab %}

### How to add resource options within editor template

The resource field can be added within editor template with multiselect control for allow multiple resources.

{% tab template="schedule/resource-field", iframeHeight="588px", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { MultiSelect } from '@syncfusion/ej2-dropdowns';
import { DateTimePicker } from '@syncfusion/ej2-calendars';
import { isNullOrUndefined } from '@syncfusion/ej2-base'
import { ScheduleComponent, EventSettingsModel, DayService, WeekService, WorkWeekService, MonthService, PopupOpenEventArgs, GroupModel } from '@syncfusion/ej2-angular-schedule';
import { eventData } from './datasource.ts';
@Component({
    selector: 'app-root',
    providers: [DayService, WeekService, WorkWeekService, MonthService],
    // specifies the template string for the Schedule component
    template: `<ejs-schedule #scheduleObj width='100%' height='550px' [selectedDate]='selectedDate' [views]='views'[eventSettings]='eventSettings' [showQuickInfo]='showQuickInfo' [group]='group'
    (popupOpen)='onPopupOpen($event)'>
        <e-resources>
            <e-resource field="OwnerId" title="Owner" name="Owners"
            [dataSource]="ownerDataSource"
            textField="text" idField="id" colorField="color">
            </e-resource>
        </e-resources>
        <ng-template #editorTemplate>
            <table class="custom-event-editor" width="100%" cellpadding="5">
                <tbody>
                    <tr>
                        <td class="e-textlabel">Summary</td>
                        <td colspan="4">
                            <input id="Subject" class="e-field e-input" type="text" value="" name="Subject" style="width: 100%" />
                        </td>
                    </tr>
                    <tr>
                    <td class="e-textlabel">From</td>
                        <td colspan="4">
                            <input id="StartTime" class="e-field" type="text" name="StartTime" />
                        </td>
                    </tr>
                    <tr>
                        <td class="e-textlabel">To</td>
                        <td colspan="4">
                            <input id="EndTime" class="e-field" type="text" name="EndTime" />
                        </td>
                    </tr>
                    <tr>
                        <td class="e-textlabel">Owner</td>
                        <td colspan="4">
                            <input type="text" id="OwnerId" name="OwnerId" class="e-field" style="width: 100%" />
                        </td>
                    </tr>
                    <tr>
                        <td class="e-textlabel">Reason</td>
                        <td colspan="4">
                            <textarea id="Description" class="e-field e-input" name="Description" rows="3" cols="50" style="width: 100%; height: 60px !important; resize: vertical"></textarea>
                        </td>
                    </tr>
                </tbody>
            </table>
        </ng-template>
    </ejs-schedule>`
})


export class AppComponent {
    @ViewChild('scheduleObj')
    public scheduleObj: ScheduleComponent;
    public selectedDate: Date = new Date(2018, 1, 15);
    public views: Array<string> = ['Day', 'Week', 'WorkWeek', 'Month'];
    public showQuickInfo: Boolean = false;
    public eventSettings: EventSettingsModel = {
        dataSource: eventData
    };
    public group: GroupModel = { resources: ['Owners'] };
    public ownerDataSource: Object[] = [
        { text: "Nancy", id: 1, color: "#1aaa55" },
        { text: "Smith", id: 2, color: "#7fa900" },
        { text: "Paul", id: 3, color: "#357cd2" }
    ];
    onPopupOpen(args: PopupOpenEventArgs): void {
        if (args.type === 'Editor') {
            let startElement: HTMLInputElement = args.element.querySelector('#StartTime') as HTMLInputElement;
            if (!startElement.classList.contains('e-datetimepicker')) {
                new DateTimePicker({ value: new Date(startElement.value) || new Date() }, startElement);
            }
            let endElement: HTMLInputElement = args.element.querySelector('#EndTime') as HTMLInputElement;
            if (!endElement.classList.contains('e-datetimepicker')) {
                new DateTimePicker({ value: new Date(endElement.value) || new Date() }, endElement);
            }
            let processElement: HTMLInputElement= args.element.querySelector('#OwnerId');
            if (!processElement.classList.contains('e-multiselect')) {
                let multiSelectObject: MultiSelect = new MultiSelect({
                    placeholder: 'Choose a owner',
                    fields: { text: 'text', value: 'id'},
                    dataSource: <any>this.ownerDataSource,
                    value: <string[]>((args.data.OwnerId instanceof Array) ? args.data.OwnerId : [args.data.OwnerId])
                });
                multiSelectObject.appendTo(processElement);
            }
        }
    }
}
```

{% endtab %}

### How to add recurrence options within editor template

The following code example shows how to add recurrence options within the editor template by importing `RecurrenceEditor`.

{% tab template="schedule/resource-field", iframeHeight="588px", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { DateTimePicker } from '@syncfusion/ej2-calendars';
import { EventSettingsModel, DayService, WeekService, WorkWeekService, MonthService, PopupOpenEventArgs, RecurrenceEditor, ScheduleComponent } from '@syncfusion/ej2-angular-schedule';
import { eventData } from './datasource.ts';
@Component({
    selector: 'app-root',
    providers: [DayService, WeekService, WorkWeekService, MonthService],
    // specifies the template string for the Schedule component
    template: `<ejs-schedule #scheduleObj width='100%' height='550px' [selectedDate]='selectedDate' [views]='views' [eventSettings]='eventSettings' [showQuickInfo]='showQuickInfo' (popupOpen)='onPopupOpen($event)'>
        <ng-template #editorTemplate>
            <table class="custom-event-editor" width="100%" cellpadding="5">
                <tbody>
                    <tr>
                        <td class="e-textlabel">Summary</td>
                        <td colspan="4">
                            <input id="Subject" class="e-field e-input" type="text" value="" name="Subject" style="width: 100%" />
                        </td>
                    </tr>
                    <tr>
                    <td class="e-textlabel">From</td>
                        <td colspan="4">
                            <input id="StartTime" class="e-field" type="text" name="StartTime" />
                        </td>
                    </tr>
                    <tr>
                        <td class="e-textlabel">To</td>
                        <td colspan="4">
                            <input id="EndTime" class="e-field" type="text" name="EndTime" />
                        </td>
                    </tr>
                    <tr>
                        <td colspan="4">
                            <div id='RecurrenceEditor'></div>
                        </td>
                    </tr>
                    <tr>
                        <td class="e-textlabel">Reason</td>
                        <td colspan="4">
                            <textarea id="Description" class="e-field e-input" name="Description" rows="3" cols="50" style="width: 100%; height: 60px !important; resize: vertical"></textarea>
                        </td>
                    </tr>
                </tbody>
            </table>
        </ng-template>
    </ejs-schedule>`
})


export class AppComponent {
    @ViewChild('scheduleObj')
    public scheduleObj: ScheduleComponent;
    public selectedDate: Date = new Date(2018, 1, 15);
    public views: Array<string> = ['Day', 'Week', 'WorkWeek', 'Month'];
    public showQuickInfo: Boolean = false;
    public eventSettings: EventSettingsModel = {
        dataSource: eventData
    };
    onPopupOpen(args: PopupOpenEventArgs): void {
        if (args.type === 'Editor') {
            let startElement: HTMLInputElement = args.element.querySelector('#StartTime') as HTMLInputElement;
            if (!startElement.classList.contains('e-datetimepicker')) {
                new DateTimePicker({ value: new Date(startElement.value) || new Date() }, startElement);
            }
            let endElement: HTMLInputElement = args.element.querySelector('#EndTime') as HTMLInputElement;
            if (!endElement.classList.contains('e-datetimepicker')) {
                new DateTimePicker({ value: new Date(endElement.value) || new Date() }, endElement);
            }
            let recurElement: HTMLElement = args.element.querySelector('#RecurrenceEditor');
            if (!recurElement.classList.contains('e-recurrenceeditor')) {
                let recurrObject: RecurrenceEditor = new RecurrenceEditor({
                });
                recurrObject.appendTo(recurElement);
                (this.scheduleObj.eventWindow as any).recurrenceEditor = recurrObject;
            }
            document.getElementById('RecurrenceEditor').style.display = (this.scheduleObj.currentAction == "EditOccurrence") ? 'none' : 'block';
        }
    }
}
```

{% endtab %}

### Apply validations on editor template fields

In the following code example, validation has been added to the status field.

{% tab template="schedule/resource-field", iframeHeight="588px", sourceFiles="app/**/*.ts" %}

```typescript
import { Component} from '@angular/core';
import { DateTimePicker } from '@syncfusion/ej2-calendars';
import { DropDownList } from '@syncfusion/ej2-dropdowns';
import { FormValidator } from '@syncfusion/ej2-inputs';
import { isNullOrUndefined } from '@syncfusion/ej2-base';
import { EventSettingsModel, DayService, WeekService, WorkWeekService, MonthService, PopupOpenEventArgs, EJ2Instance} from '@syncfusion/ej2-angular-schedule';
import { eventData } from './datasource.ts';
@Component({
    selector: 'app-root',
    providers: [DayService, WeekService, WorkWeekService, MonthService],
    // specifies the template string for the Schedule component
    template: `<ejs-schedule width='100%' height='550px' [selectedDate]='selectedDate' [views]='views' [eventSettings]='eventSettings' [showQuickInfo]='showQuickInfo' (popupOpen)='onPopupOpen($event)'>
        <ng-template #editorTemplate>
            <table class="custom-event-editor" width="100%" cellpadding="5">
                <tbody>
                    <tr>
                        <td class="e-textlabel">Summary</td>
                        <td colspan="4">
                            <input id="Subject" class="e-field e-input" type="text" value="" name="Subject" style="width: 100%" />
                        </td>
                    </tr>
                    <tr>
                        <td class="e-textlabel">Status</td>
                        <td colspan="4">
                            <input type="text" id="EventType" name="EventType" class="e-field" style="width: 100%" />
                        </td>
                    </tr>
                    <tr>
                    <td class="e-textlabel">From</td>
                        <td colspan="4">
                            <input id="StartTime" class="e-field" type="text" name="StartTime" />
                        </td>
                    </tr>
                    <tr>
                        <td class="e-textlabel">To</td>
                        <td colspan="4">
                            <input id="EndTime" class="e-field" type="text" name="EndTime" />
                        </td>
                    </tr>
                    <tr>
                        <td class="e-textlabel">Reason</td>
                        <td colspan="4">
                            <textarea id="Description" class="e-field e-input" name="Description" rows="3" cols="50"
                                style="width: 100%; height: 60px !important; resize: vertical"></textarea>
                        </td>
                    </tr>
                </tbody>
            </table>
        </ng-template>
    </ejs-schedule>`
})


export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public views: Array<string> = ['Day', 'Week', 'WorkWeek', 'Month'];
    public showQuickInfo: Boolean = false;
    public eventSettings: EventSettingsModel = {
        dataSource: eventData
    };
    onPopupOpen(args: PopupOpenEventArgs): void {
        if (args.type === 'Editor') {
            if (!isNullOrUndefined(document.getElementById("EventType_Error"))) {
                document.getElementById("EventType_Error").style.display = "none";
                document.getElementById("EventType_Error").style.left = "351px";
            }
            let formElement: HTMLElement = <HTMLElement>args.element.querySelector('.e-schedule-form');
            let statusElement: HTMLInputElement = args.element.querySelector('#EventType') as HTMLInputElement;
            if (!statusElement.classList.contains('e-dropdownlist')) {
                let dropDownListObject: DropDownList = new DropDownList({
                    placeholder: 'Choose status', value: statusElement.value,
                    dataSource: ['New', 'Requested', 'Confirmed'],
                    select: function(args) {
                        if (!isNullOrUndefined(document.getElementById("EventType_Error"))) {
                            document.getElementById("EventType_Error").style.display = "none";
                        }
                    }
                });
                dropDownListObject.appendTo(statusElement);
                statusElement.setAttribute('name', 'EventType');
            }
            let validator: FormValidator = ((formElement as EJ2Instance).ej2_instances[0] as FormValidator);
            validator.addRules('EventType', { required: true });
            let startElement: HTMLInputElement = args.element.querySelector('#StartTime') as HTMLInputElement;
            if (!startElement.classList.contains('e-datetimepicker')) {
                new DateTimePicker({ value: new Date(startElement.value) || new Date() }, startElement);
            }
            let endElement: HTMLInputElement = args.element.querySelector('#EndTime') as HTMLInputElement;
            if (!endElement.classList.contains('e-datetimepicker')) {
                new DateTimePicker({ value: new Date(endElement.value) || new Date() }, endElement);
            }
        }
    }
}
```

{% endtab %}

### How to save the customized event editor using template

The **e-field** class is not added to each field defined within the template, so you should allow to set those field values externally by using the `popupClose` event.

Note: You can allow to retrieve the data only on the `save` and `delete` option. Data cannot be retrieved on the `close` and `cancel` options in the editor window.

The following code example shows how to save the customized event editor using a template by the `popupClose` event.

{% tab template="schedule/resource-field", iframeHeight="588px", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { DropDownList } from '@syncfusion/ej2-dropdowns';
import { DateTimePicker } from '@syncfusion/ej2-calendars';
import { isNullOrUndefined } from '@syncfusion/ej2-base';
import { EventSettingsModel, DayService, WeekService, WorkWeekService, MonthService, PopupOpenEventArgs, PopupCloseEventArgs } from '@syncfusion/ej2-angular-schedule';
import { eventData } from './datasource.ts';
@Component({
    selector: 'app-root',
    providers: [DayService, WeekService, WorkWeekService, MonthService],
    // specifies the template string for the Schedule component
    template: `<ejs-schedule width='100%' height='550px' [selectedDate]='selectedDate' [views]='views' [eventSettings]='eventSettings' [showQuickInfo]='showQuickInfo' (popupOpen)='onPopupOpen($event)' (popupClose) ='onPopupClose($event)'>
    <ng-template #editorTemplate>
        <table class="custom-event-editor" width="100%" cellpadding="5">
            <tbody>
                <tr>
                    <td class="e-textlabel">Summary</td>
                    <td colspan="4">
                        <input id="Subject" class="e-input" type="text" name="Subject" style="width: 100%" />
                    </td>
                </tr>
                <tr>
                    <td class="e-textlabel">Status</td>
                    <td colspan="4">
                        <input type="text" id="EventType" name="EventType" style="width: 100%" />
                    </td>
                </tr>
                <tr>
                    <td class="e-textlabel">From</td>
                    <td colspan="4">
                        <input id="StartTime" type="text" name="StartTime" />
                    </td>
                </tr>
                <tr>
                    <td class="e-textlabel">To</td>
                    <td colspan="4">
                        <input id="EndTime" type="text" name="EndTime" />
                    </td>
                </tr>
                <tr>
                    <td class="e-textlabel">Reason</td>
                    <td colspan="4">
                        <textarea id="Description" class="e-input" name="Description" rows="3" cols="50" style="width: 100%; height: 60px !important; resize: vertical"></textarea>
                    </td>
                </tr>
            </tbody>
        </table>
    </ng-template>
    </ejs-schedule>`
})

export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public views: Array<string> = ['Day', 'Week', 'WorkWeek', 'Month'];
    public showQuickInfo: Boolean = false;
    public eventSettings: EventSettingsModel = {
        dataSource: eventData
    };
    onPopupOpen(args: PopupOpenEventArgs) : void {
        if (args.type === 'Editor') {
            let subjectElement: HTMLInputElement = args.element.querySelector('#Subject') as HTMLInputElement;
            if (subjectElement) {
                subjectElement.value = ((<{ [key: string]: Object }>(args.data)).Subject as string) || "";
            }
            let statusElement: HTMLInputElement = args.element.querySelector('#EventType') as HTMLInputElement;
            if (!statusElement.classList.contains('e-dropdownlist')) {
                let dropDownListObject: DropDownList = new DropDownList({
                    placeholder: 'Choose status', value: ((<{ [key: string]: Object }>(args.data)).EventType as string),
                    dataSource: ['New', 'Requested', 'Confirmed']
                });
                dropDownListObject.appendTo(statusElement);
            }
            let startElement: HTMLInputElement = args.element.querySelector('#StartTime') as HTMLInputElement;
            if (!startElement.classList.contains('e-datetimepicker')) {
                startElement.value = (<{ [key: string]: Object }>(args.data)).StartTime as string;
                new DateTimePicker({ value: new Date(startElement.value) || new Date() }, startElement);
            }
            let endElement: HTMLInputElement = args.element.querySelector('#EndTime') as HTMLInputElement;
            if (!endElement.classList.contains('e-datetimepicker')) {
                endElement.value = (<{ [key: string]: Object }>(args.data)).EndTime as string;
                new DateTimePicker({ value: new Date(endElement.value) || new Date() }, endElement);
            }
            let descriptionElement: HTMLInputElement = args.element.querySelector('#Description') as HTMLInputElement;
            if (descriptionElement) {
                descriptionElement.value = (<{ [key: string]: Object }>(args.data)).Description as string || "";
            }
        }
    }
    onPopupClose(args: PopupCloseEventArgs) : void {
        if (args.type === 'Editor' && !isNullOrUndefined(args.data)) {
            let subjectElement: HTMLInputElement = args.element.querySelector('#Subject') as HTMLInputElement;
            if (subjectElement ) {
                (<{ [key: string]: Object }>(args.data)).Subject = subjectElement.value;
            }
            let statusElement: HTMLInputElement = args.element.querySelector('#EventType') as HTMLInputElement;
            if (statusElement) {
                ((<{ [key: string]: Object }>(args.data)).EventType as string) = statusElement.value;
            }
            let startElement: HTMLInputElement = args.element.querySelector('#StartTime') as HTMLInputElement;
            if (startElement) {
                (<{ [key: string]: Object }>(args.data)).StartTime = startElement.value;
            }
            let endElement: HTMLInputElement = args.element.querySelector('#EndTime') as HTMLInputElement;
            if (endElement) {
                (<{ [key: string]: Object }>(args.data)).EndTime = endElement.value;
            }
            let descriptionElement: HTMLInputElement = args.element.querySelector('#Description') as HTMLInputElement;
            if (descriptionElement) {
                ((<{ [key: string]: Object }>(args.data)).Description as string) = descriptionElement.value;
            }
        }
    }
}
```

{% endtab %}

In case, if you need to prevent only specific popups on Scheduler, then you can check the condition based on the popup type. The types of the popup that can be checked within the `popupClose` event are as follows.

| Type | Description |
|------|-------------|
| Editor | For Detailed editor window.|
| QuickInfo | For Quick popup which opens on cell click.|
| EditEventInfo |For  Quick popup which opens on event click.|
| ViewEventInfo | For Quick popup which opens on responsive mode.|
| EventContainer | For more event indicator popup.|
| RecurrenceAlert | For edit recurrence event alert popup.|
| DeleteAlert | For delete confirmation popup.|
| ValidationAlert | For validation alert popup.|
| RecurrenceValidationAlert | For recurrence validation alert popup.|

### How to enable save button in customized event editor using template

Initially **e-custom-disable** class is added to the save button once all the fields are filled **e-custom-disable** class is removed from the save button.

The following code example shows how to enable save button in customized event editor using a template by the `keyup` and `change` event.

{% tab template="schedule/resource-field", iframeHeight="588px", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from "@angular/core";
import { extend } from "@syncfusion/ej2-base";
import { DropDownList } from "@syncfusion/ej2-dropdowns";
import { DateTimePicker } from "@syncfusion/ej2-calendars";
import { FormValidators, FormValidator, TextBox } from "@syncfusion/ej2-angular-inputs";
import { PopupOpenEventArgs, EventRenderedArgs, ScheduleComponent, MonthService, DayService, WeekService,
  WorkWeekService, EventSettingsModel, ResizeService, DragAndDropService, EJ2Instance
} from "@syncfusion/ej2-angular-schedule";
import { eventData } from './datasource.ts';
@Component({
    selector: 'app-root',
    providers: [ MonthService, DayService, WeekService, WorkWeekService, ResizeService, DragAndDropService],
    encapsulation: ViewEncapsulation.None,
    // specifies the template string for the Schedule component
    template: `<ejs-schedule width='100%' height='550px' [selectedDate]='selectedDate' [views]='views' [eventSettings]='eventSettings' [showQuickInfo]='showQuickInfo' (popupOpen)='onPopupOpen($event)' >
    <ng-template #editorTemplate>
        <table class="custom-event-editor" width="100%" cellpadding="5">
            <tbody>
                <tr>
                    <td class="e-textlabel">Summary</td>
                    <td colspan="4">
                        <input id="Subject" class=" e-field e-input" type="text" name="Subject" value="" style="width: 100%" (keyup)="onChange($event)" />
                    </td>
                </tr>
                <tr>
                    <td class="e-textlabel">Status</td>
                    <td colspan="4">
                        <input type="text" id="EventType" class="e-field" name="EventType" style="width: 100%" (change)="onChange($event)" />
                    </td>
                </tr>
                <tr>
                    <td class="e-textlabel">From</td>
                    <td colspan="4">
                        <input id="StartTime" class="e-field" type="text" name="StartTime" />
                    </td>
                </tr>
                <tr>
                    <td class="e-textlabel">To</td>
                    <td colspan="4">
                        <input id="EndTime" class="e-field" type="text" name="EndTime" />
                    </td>
                </tr>
                <tr>
                    <td class="e-textlabel">Reason</td>
                    <td colspan="4">
                        <textarea id="Description" class="e-field e-input" name="Description" rows="3" cols="50" style="width: 100%; height: 60px !important; resize: vertical" (keyup)="onChange($event)"></textarea>
                    </td>
                </tr>
            </tbody>
        </table>
    </ng-template>
    </ejs-schedule>`
})

export class AppComponent {
  @ViewChild("scheduleObj") scheduleObj: ScheduleComponent;
  public selectedDate: Date = new Date(2018, 1, 15);
  public views: Array<string> = ['Day', 'Week', 'WorkWeek', 'Month'];
  public showQuickInfo: Boolean = false;
  public eventSettings: EventSettingsModel = {
    dataSource: eventData,
    fields: {
      subject: { name: "Subject", validation: { required: true } },
      description: {
        name: "Description",
        validation: { required: true }
      }
    }
  };
  public validator: FormValidator;
  public statusFields: Object = { text: "StatusText", value: "StatusText" };
  public StatusData: Object[] = [
    { StatusText: "New", Id: 1 },
    { StatusText: "Requested", Id: 2 },
    { StatusText: "Confirmed", Id: 3 }
  ];

  private onPopupOpen(args: PopupOpenEventArgs): void {
    if (args.type === "Editor") {
        let subjectElement: HTMLInputElement = args.element.querySelector('#Subject') as HTMLInputElement;
        let subjectElement: HTMLInputElement = args.element.querySelector('#Subject') as HTMLInputElement;
        if (subjectElement) {
            subjectElement.value = ((<{ [key: string]: Object }>(args.data)).Subject as string) || "";
         }
        let statusElement: HTMLInputElement = args.element.querySelector('#EventType') as HTMLInputElement;
        if (!statusElement.classList.contains('e-dropdownlist')) {
            let dropDownListObject: DropDownList = new DropDownList({
                placeholder: 'Choose status', value: ((<{ [key: string]: Object }>(args.data)).EventType as string),
                    dataSource: ['New', 'Requested', 'Confirmed']
            });
            dropDownListObject.appendTo(statusElement);
        }
        let startElement: HTMLInputElement = args.element.querySelector('#StartTime') as HTMLInputElement;
        if (!startElement.classList.contains('e-datetimepicker')) {
            startElement.value = (<{ [key: string]: Object }>(args.data)).StartTime as string;
            new DateTimePicker({ value: new Date(startElement.value) || new Date() }, startElement);
        }
        let endElement: HTMLInputElement = args.element.querySelector('#EndTime') as HTMLInputElement;
        if (!endElement.classList.contains('e-datetimepicker')) {
            endElement.value = (<{ [key: string]: Object }>(args.data)).EndTime as string;
            new DateTimePicker({ value: new Date(endElement.value) || new Date() }, endElement);
        }
        let descriptionElement: HTMLInputElement = args.element.querySelector('#Description') as HTMLInputElement;
        if (descriptionElement) {
            descriptionElement.value = (<{ [key: string]: Object }>(args.data)).Description as string || "";
        }
      const formElement: HTMLElement = args.element.querySelector(".e-schedule-form") as HTMLElement;
      this.validator = (formElement as EJ2Instance).ej2_instances[0] as FormValidator;
      this.validator.addRules("EventType", { required: [true, "This field is required."]});
      if (args.target.classList.contains("e-work-cells")) {
        args.element.querySelector(".e-event-save").classList.add("e-custom-disable");
      }
    }
  }

  public onChange(args) {
    let form = (document.querySelector(".e-schedule-form") as any).ej2_instances[0];
    if (args.element && !args.e) {
      return;
    }
    let names = ["Subject", "Description", "EventType"];
    names.forEach(e => {
      form.validateRules(e);
    });
    let isValidated = false;
    let errorElements = document.querySelector(".e-dlg-content").querySelectorAll(".e-schedule-error");
    for (let i = 0; i < errorElements.length; i++) {
      isValidated =(errorElements[i] as any).style.display === "none" ? true : false;
      if (isValidated === false) {
        break;
      }
    }
    let saveBtn = document.querySelector(".e-custom-disable");
    if (isValidated && saveBtn) {
      saveBtn.classList.remove("e-custom-disable");
    } else if (!isValidated && !saveBtn) {
      document.querySelector(".e-event-save").classList.add("e-custom-disable");
    }
  }
}
```

{% endtab %}

## Quick popups

The quick info popups are the ones that gets opened, when a cell or appointment is single clicked on the desktop mode. On single clicking a cell, you can simply provide a subject and save it. Also, while single clicking on an event, a popup will be displayed where you can get the overview of the event information. You can also edit or delete those events through the options available in it.

By default, these popups are displayed over cells and appointments of Scheduler and to disable this action, set `false` to `showQuickInfo` property.

> The quick popup that opens while single clicking on the cells are not applicable on mobile devices.

{% tab template="schedule/editor-window", iframeHeight="588px", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, DayService, WeekService, WorkWeekService, MonthService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource.ts';
@Component({
    selector: 'app-root',
    providers: [DayService, WeekService, WorkWeekService, MonthService],
    // specifies the template string for the Schedule component
    template: `<ejs-schedule width='100%' height='550px' [selectedDate]='selectedDate' [views]='views' [eventSettings]='eventSettings' [showQuickInfo]='showQuickInfo'></ejs-schedule>`
})


export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public views: Array<string> = ['Day', 'Week', 'WorkWeek', 'Month'];
    public showQuickInfo: Boolean = false;
    public eventSettings: EventSettingsModel = {
        dataSource: scheduleData
    };
}
```

{% endtab %}

### How to change the watermark text of quick popup subject

By default, `Add Title` text is displayed on the subject field of quick popup. To change the default watermark text, change the value of the appropriate localized word collection used in the Scheduler.

```typescript
L10n.load({
    'en-US': {
        'schedule': {
          'addTitle' : 'New Title'
        }
    }
});
```

### Customizing quick popups

The look and feel of the built-in quick popup window, which opens when single clicked on the cells or appointments can be customized by making use of the `quickInfoTemplates` property of the Scheduler. There are 3 sub-options available to customize them easily,

* header - Accepts the template design that customizes the header part of the quick popup.
* content - Accepts the template design that customizes the content part of the quick popup.
* footer - Accepts the template design that customizes the footer part of the quick popup.

{% tab template="schedule/quick-popup", iframeHeight="588px", sourceFiles="app/**/*.ts,app/index.css" %}

```typescript
import { Component, ViewChild, ViewEncapsulation } from '@angular/core';
import { isNullOrUndefined } from '@syncfusion/ej2-base';
import { ScheduleComponent, CurrentAction, EventSettingsModel, DayService, WeekService, WorkWeekService, MonthService, PopupOpenEventArgs } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource.ts';
@Component({
    selector: 'app-root',
    providers: [DayService, WeekService, WorkWeekService, MonthService],
    // specifies the template string for the Schedule component
    template: `<ejs-schedule #scheduleObj width='100%' height='550px' [selectedDate]="selectedDate" [eventSettings]="eventSettings"
    (popupOpen)="onPopupOpen($event)">

    <!-- Header template -->
    <ng-template #quickInfoTemplatesHeader let-data>
      <div *ngIf="data.elementType == 'cell' || data.elementType == 'event'">
        <div class="e-popup-header">
          <div class="e-header-icon-wrapper">
            <div *ngIf="data.elementType == 'event'" class="subject">{{data.Subject}}</div>
            <button class="e-close e-close-icon e-icons" title="Close" (click)="onCloseClick($event)"></button>
          </div>
        </div>
      </div>
    </ng-template>

    <!-- Content Template -->
    <ng-template #quickInfoTemplatesContent let-data>
      <div *ngIf="data.elementType == 'cell'" class="e-cell-content">
        <form class="e-schedule-form">
          <div style="padding:10px">
            <input class="subject e-field e-input" type="text" name="Subject" placeholder="Title" style="width:100%">
          </div>
          <div style="padding:10px">
            <input class="location e-field e-input" type="text" name="Location" placeholder="Location" style="width:100%">
          </div>
        </form>
      </div>
      <div *ngIf="data.elementType == 'event'" class="e-event-content">
        <div class="start-time">Start: {{data.StartTime.toLocaleString()}}</div>
        <div class="end-time">End: {{data.EndTime.toLocaleString()}}</div>
        <div *ngIf="data.Location != undefined && data.Location != ''" class="location">Location: {{data.Location}}</div>
      </div>
    </ng-template>

    <!-- Footer Template -->
    <ng-template #quickInfoTemplatesFooter let-data>
      <div *ngIf="data.elementType == 'cell'" class="e-cell-footer">
        <div class="left-button">
          <button class="e-event-details" title="Extra Details" (click)="onDetailsClick($event)">More Details</button>
        </div>
        <div class="right-button">
          <button class="e-event-create" title="Add" (click)="onAddClick($event)">Add</button>
        </div>
      </div>
      <div *ngIf="data.elementType == 'event'" class="e-event-footer">
        <div class="left-button">
          <button class="e-delete" title="Delete" (click)="onDeleteClick($event)">Delete</button>
          <button *ngIf="data.RecurrenceRule != undefined && data.RecurrenceRule != ''" class="e-delete-series"
            title="Delete" (click)="onDeleteClick($event)">Delete Series</button>
        </div>
        <div class="right-button">
          <button class="e-edit" title="Edit" (click)="onEditClick($event)">Edit</button>
          <button *ngIf="data.RecurrenceRule != undefined && data.RecurrenceRule != ''" class="e-edit-series"
            title="Edit" (click)="onEditClick($event)">Edit Series</button>
        </div>
      </div>
    </ng-template>
  </ejs-schedule>`,
    styleUrls: ['app/index.css'],
    encapsulation: ViewEncapsulation.None,
})


export class AppComponent {
    @ViewChild('scheduleObj')
    public scheduleObj: ScheduleComponent;
    public eventSettings: EventSettingsModel = {
        dataSource: scheduleData
    };
    public selectedDate: Date = new Date(2018, 1, 15);
    private selectionTarget: Element;
    public onPopupOpen(args: PopupOpenEventArgs): void {
        this.selectionTarget = null;
        this.selectionTarget = args.target;
    }
    public onDetailsClick(): void {
        this.onCloseClick();
        const data: Object = this.scheduleObj.getCellDetails(this.scheduleObj.getSelectedElements()) as Object;
        this.scheduleObj.openEditor(data, 'Add');
    }
    public onAddClick(): void {
        this.onCloseClick();
        const data: Object = this.scheduleObj.getCellDetails(this.scheduleObj.getSelectedElements()) as Object;
        const eventData: { [key: string]: Object } = this.scheduleObj.eventWindow.getObjectFromFormData('e-quick-popup-wrapper');
        this.scheduleObj.eventWindow.convertToEventData(data as { [key: string]: Object }, eventData);
        eventData.Id = this.scheduleObj.eventBase.getEventMaxID() as number + 1;
        this.scheduleObj.addEvent(eventData);
    }
    public onEditClick(args: any): void {
        if (this.selectionTarget) {
        let eventData: { [key: string]: Object } = this.scheduleObj.getEventDetails(this.selectionTarget) as { [key: string]: Object };
        let currentAction: CurrentAction = 'Save';
        if (!isNullOrUndefined(eventData.RecurrenceRule) && eventData.RecurrenceRule !== '') {
            if (args.target.classList.contains('e-edit-series')) {
            currentAction = 'EditSeries';
            eventData = this.scheduleObj.eventBase.getParentEvent(eventData, true);
            } else {
            currentAction = 'EditOccurrence';
            }
        }
        this.scheduleObj.openEditor(eventData, currentAction);
        }
    }
    public onDeleteClick(args: any): void {
        this.onCloseClick();
        if (this.selectionTarget) {
        const eventData: { [key: string]: Object } = this.scheduleObj.getEventDetails(this.selectionTarget) as { [key: string]: Object };
        let currentAction: CurrentAction;
        if (!isNullOrUndefined(eventData.RecurrenceRule) && eventData.RecurrenceRule !== '') {
            currentAction = args.target.classList.contains('e-delete-series') ? 'DeleteSeries' : 'DeleteOccurrence';
        }
        this.scheduleObj.deleteEvent(eventData, currentAction);
        }
    }
    public onCloseClick(): void {
        this.scheduleObj.quickPopup.quickPopupHide();
    }
}
```

{% endtab %}

> The quick popup in adaptive mode can also be customized using `quickInfoTemplates` using `e-device` class.

## More events indicator and popup

When the number of appointments count that lies on a particular time range * default appointment height exceeds the default height of a cell in month view and all other timeline views, a `+ more` text indicator will be displayed at the bottom of those cells. This indicator denotes that the cell contains few more appointments in it and clicking on that will display a popup displaying all the appointments present on that day.

> To disable this option of showing popup with all hidden appointments, while clicking on the text indicator, you can do code customization within the `popupOpen` event.

The same indicator is displayed on all-day row in calendar views such as day, week and work week views alone, when the number of appointment count present in a cell exceeds three. Clicking on the text indicator here will not open a popup, but will allow the expand/collapse option for viewing the remaining appointments present in the all-day row.

The following code example shows how to disable the display of such popups while clicking on the more text indicator.

{% tab template="schedule/editor-window", iframeHeight="588px", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, DayService, WeekService, WorkWeekService, MonthService, PopupOpenEventArgs } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource.ts';
@Component({
    selector: 'app-root',
    providers: [DayService, WeekService, WorkWeekService, MonthService],
    // specifies the template string for the Schedule component
    template: `<ejs-schedule width='100%' height='550px' [selectedDate]='selectedDate' [views]='views' [currentView]='currentView' [eventSettings]='eventSettings' (popupOpen)='onPopupOpen($event)'></ejs-schedule>`
})


export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public views: Array<string> = ['Day', 'Week', 'WorkWeek', 'Month'];
    public currentView: string = 'Month';
    public eventSettings: EventSettingsModel = {
        dataSource: scheduleData
    };
    onPopupOpen(args: PopupOpenEventArgs): void {
        if (args.type === 'EventContainer') {
            args.cancel = true;
        }
    }
}
```

{% endtab %}

### How to customize the popup that opens on more indicator

The following code example shows you how to customize the default more indicator popup in which number of events rendered count on the day has been shown in the header.

{% tab template="schedule/editor-window", iframeHeight="588px", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';
import { Internationalization } from '@syncfusion/ej2-base';
import { EventSettingsModel, DayService, WeekService, WorkWeekService, MonthService, PopupOpenEventArgs } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource.ts';
@Component({
    selector: 'app-root',
    providers: [DayService, WeekService, WorkWeekService, MonthService],
    // specifies the template string for the Schedule component
    template: `<ejs-schedule width='100%' height='550px' [selectedDate]='selectedDate' [views]='views' [currentView]='currentView' [cssClass]='cssClass' [eventSettings]='eventSettings' (popupOpen)='onPopupOpen($event)'></ejs-schedule>`,
    styleUrls: ['app/index.css'],
    encapsulation: ViewEncapsulation.None
})


export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public views: Array<string> = ['Day', 'Week', 'WorkWeek', 'Month'];
    public currentView: string = 'Month';
    public cssClass: string = 'schedule-more-indicator';
    public eventSettings: EventSettingsModel = {
        dataSource: scheduleData
    };
    onPopupOpen(args: PopupOpenEventArgs): void {
        if (args.type === 'EventContainer') {
            let instance: Internationalization = new Internationalization();
            let date: string  = instance.formatDate((<any>args.data).date, { skeleton: 'MMMEd' });
            ((args.element.querySelector('.e-header-date')) as HTMLElement).innerText = date;
            ((args.element.querySelector('.e-header-day')) as HTMLElement).innerText = 'Event count: ' + (<any>args.data).event.length;
        }
    }
}
```

{% endtab %}

### How to prevent the display of popup when clicking on the more text indicator

It is possible to prevent the display of popup window by passing the value `true` to `cancel` option within the `MoreEventsClick` event.

{% tab template="schedule/editor-window", iframeHeight="588px", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, DayService, WeekService, WorkWeekService, MonthService, MoreEventsClickArgs } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource.ts';
@Component({
    selector: 'app-root',
    providers: [DayService, WeekService, WorkWeekService, MonthService],
    // specifies the template string for the Schedule component
    template: `<ejs-schedule width='100%' height='550px' [selectedDate]='selectedDate' [views]='views' [currentView]='currentView' [eventSettings]='eventSettings' (moreEventsClick)='onMoreEventsClick($event)'></ejs-schedule>`
})


export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public views: Array<string> = ['Day', 'Week', 'WorkWeek', 'Month'];
    public currentView: string = 'Month';
    public eventSettings: EventSettingsModel = {
        dataSource: scheduleData
    };
    onMoreEventsClick(args: MoreEventsClickArgs): void {
        args.cancel = true;
    }
}
```

{% endtab %}

### How to navigate Day view when clicking on more text indicator

The following code example shows you how to customize the `moreEventsClick` property to navigate to the Day view when clicking on the more text indicator.

{% tab template="schedule/editor-window", iframeHeight="588px", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, DayService, WeekService, WorkWeekService, MonthService, MoreEventsClickArgs } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource.ts';
@Component({
    selector: 'app-root',
    providers: [DayService, WeekService, WorkWeekService, MonthService],
    // specifies the template string for the Schedule component
    template: `<ejs-schedule width='100%' height='550px' [selectedDate]='selectedDate' [views]='views' [currentView]='currentView' [eventSettings]='eventSettings' (moreEventsClick)='onMoreEventsClick($event)'></ejs-schedule>`
})


export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public views: Array<string> = ['Day', 'Week', 'WorkWeek', 'Month'];
    public currentView: string = 'Month';
    public eventSettings: EventSettingsModel = {
        dataSource: scheduleData
    };
    onMoreEventsClick(args: MoreEventsClickArgs): void {
        args.isPopupOpen = false;
    }
}

```

{% endtab %}