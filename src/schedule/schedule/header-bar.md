---
title: "Scheduler Header customization"
component: "Scheduler"
description: "This section explains how to customize the header bar of Scheduler and to add custom items into it."
---

# Header customization

The header part of Scheduler can be customized easily with the built-in options available.

## Show or Hide header bar

By default, the header bar holds the date and view navigation options, through which the user can switch between the dates and various views. This header bar can be hidden from the UI by setting `false` to the `showHeaderBar` property. It's default value is `true`.

{% tab template="schedule/header-bar", iframeHeight="588px", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, DayService, WeekService, WorkWeekService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource.ts';
@Component({
    selector: 'app-root',
    providers: [DayService, WeekService, WorkWeekService],
    // specifies the template string for the Schedule component
    template: `<ejs-schedule width='100%' height='550px' [selectedDate]='selectedDate' [views]='views'[eventSettings]='eventSettings' [showHeaderBar]='showHeaderBar'>
    </ejs-schedule>`
})


export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public views: Array<string> = ['Day', 'Week', 'WorkWeek'];
    public eventSettings: EventSettingsModel = {
        dataSource: scheduleData
    };
    public showHeaderBar: Boolean = false;
}
```

{% endtab %}

## Customizing header bar

Apart from the default date navigation and view options available on the header bar, you can add custom items into the Scheduler header bar by making use of the `actionBegin` event. Here, an employee image is added to the header bar, clicking on which will open the popup showing that person's short profile information.

{% tab template="schedule/header-bar", iframeHeight="588px", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { createElement, compile } from '@syncfusion/ej2-base';
import { ItemModel } from '@syncfusion/ej2-navigations';
import { Popup } from '@syncfusion/ej2-popups';
import { EventSettingsModel, ActionEventArgs, ToolbarActionArgs, MonthService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource.ts';

@Component({
    selector: 'app-root',
    providers: [MonthService],
    // specifies the template string for the Schedule component
    template: `<ejs-schedule id='schedule' width='100%' height='550px' [selectedDate]='selectedDate' [views]='views' [eventSettings]='eventSettings' [showHeaderBar]='showHeaderBar'
    [currentView]='currentView' (actionBegin)='onActionBegin($event)'
    (actionComplete)='onActionComplete($event)'></ejs-schedule>`
})


export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public views: Array<string> = ['Month'];
    public currentView: string = 'Month';
    public eventSettings: EventSettingsModel = {
        dataSource: scheduleData
    };
    public userContentEle: HTMLElement = createElement('div', {
        className: 'e-profile-wrapper'
    });
    public profilePopup: Popup;
    onActionBegin(args: ActionEventArgs & ToolbarActionArgs):void {
        if (args.requestType === 'toolbarItemRendering') {
            let userIconItem: ItemModel = {
                align: 'Right', prefixIcon: 'user-icon', text: 'Nancy', cssClass: 'e-schedule-user-icon'
            };
            args.items.push(userIconItem);
        }
    }
    onActionComplete(args: ActionEventArgs):void {
        let scheduleElement: HTMLElement = document.getElementById('schedule') as HTMLElement;
        if (args.requestType === 'toolBarItemRendered') {
            let userIconEle: HTMLElement = scheduleElement.querySelector('.e-schedule-user-icon') as HTMLElement;
            userIconEle.onclick = () => {
                this.profilePopup.relateTo = userIconEle;
                this.profilePopup.dataBind();
                if (this.profilePopup.element.classList.contains('e-popup-close')) {
                    this.profilePopup.show();
                } else {
                    this.profilePopup.hide();
                }
            };
        }

        let userContentEle: HTMLElement = createElement('div', {
            className: 'e-profile-wrapper'
        });
        scheduleElement.parentElement.appendChild(userContentEle);

        let userIconEle: HTMLElement = scheduleElement.querySelector('.e-schedule-user-icon') as HTMLElement;
        let getDOMString: (data: object) => NodeList = compile('<div class="profile-container"><div class="profile-image">' +
            '</div><div class="content-wrap"><div class="name">Nancy</div>' +
            '<div class="destination">Product Manager</div><div class="status">' +
            '<div class="status-icon"></div>Online</div></div></div>');
        let output: NodeList = getDOMString({});
        this.profilePopup = new Popup(userContentEle, {
            content: output[0] as HTMLElement,
            relateTo: userIconEle,
            position: { X: 'left', Y: 'bottom' },
            collision: { X: 'flip', Y: 'flip' },
            targetType: 'relative',
            viewPortElement: scheduleElement,
            width: 185,
            height: 80
        });
        this.profilePopup.hide();
    }
}
```

{% endtab %}

## How to display the view options within the header bar popup

By default, the header bar holds the view navigation options, through which the user can switch between various views. You can move this view options to the header bar popup by setting `true` to the `enableAdaptiveUI` property.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, DayService, WeekService, WorkWeekService, MonthService, AgendaService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource.ts';

@Component({
    selector: 'app-root',
    providers: [DayService, WeekService, WorkWeekService, MonthService, AgendaService],
    // specifies the template string for the Schedule component
    template: `<ejs-schedule width='100%' height='550px' [selectedDate]="selectedDate"
  [eventSettings]="eventSettings" [enableAdaptiveUI]="enableAdaptiveUI"></ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public eventSettings: EventSettingsModel = {
        dataSource: scheduleData,
    };
    public enableAdaptiveUI: true;
}
```

{% endtab %}

> Refer [here](./resources/#adaptive-ui-in-desktop) to know more about adaptive UI in resources scheduler.

## Date header customization

The Scheduler UI that displays the date text on all views are considered as the date header cells. You can customize the date header cells of Scheduler either using `dateHeaderTemplate` or `renderCell` event.

### Using date header template

The `dateHeaderTemplate` option is used to customize the date header cells of day, week and work-week views.

{% tab template="schedule/header-bar", iframeHeight="588px", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';
import { Internationalization } from '@syncfusion/ej2-base';
import { EventSettingsModel, DayService, WeekService, AgendaService, TimelineViewsService, TimelineMonthService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource.ts';
@Component({
    selector: 'app-root',
    providers: [DayService, WeekService, AgendaService, TimelineViewsService, TimelineMonthService],
    // specifies the template string for the Schedule component
    template: `<ejs-schedule id='schedule' width='100%' height='550px' [cssClass]='cssClass'
    [selectedDate]='selectedDate' [views]='views' [eventSettings]='eventSettings'>
    <ng-template #dateHeaderTemplate let-data>
        <div class="date-text">{{getDateHeaderText(data.date)}}</div>
        <div [innerHTML]="getWeather(data.date)"></div>
    </ng-template>
    </ejs-schedule>`,
    styles: [`.weather-text {
        padding: 5px;
        color: #e3165b;
        font-weight: 500;
    }`],
    encapsulation: ViewEncapsulation.None
})


export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public views: Array<string> = ['Day', 'Week', 'Agenda', 'TimelineWorkWeek', 'TimelineMonth'];
    public eventSettings: EventSettingsModel = {
        dataSource: scheduleData
    };
    public cssClass: string = 'schedule-date-header-template';
    public instance: Internationalization = new Internationalization();
    getDateHeaderText: Function = (value: Date) => {
        return this.instance.formatDate(value, { skeleton: 'Ed' });
    };
    getWeather: Function = (value: Date) => {
        switch (value.getDay()) {
            case 0:
                return '<div class="weather-text">25°C</div>';
            case 1:
                return '<div class="weather-text">18°C</div>';
            case 2:
                return '<div class="weather-text">10°C</div>';
            case 3:
                return '<div class="weather-text">16°C</div>';
            case 4:
                return '<div class="weather-text">8°C</div>';
            case 5:
                return '<div class="weather-text">27°C</div>';
            case 6:
                return '<div class="weather-text">17°C</div>';
            default:
                return null;
        }
    }
}
```

{% endtab %}

### Using renderCell event

In month view, the date header template is not applicable and therefore the same customization can be added beside the date text in month cells by making use of the `renderCell` event.

{% tab template="schedule/header-bar", iframeHeight="588px", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';
import { EventSettingsModel, MonthService, RenderCellEventArgs } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource.ts';
@Component({
    selector: 'app-root',
    providers: [MonthService],
    // specifies the template string for the Schedule component
    template: `<ejs-schedule id='schedule' width='100%' height='550px' [cssClass]='cssClass' [selectedDate]='selectedDate' [views]='views' [eventSettings]='eventSettings'
    (renderCell)='onRenderCell($event)'></ejs-schedule>`,
    styles: [`.weather-text {
        float: right;
        margin: -20px 2px 0 0;
        color: #EA7A57;
    }`],
    encapsulation: ViewEncapsulation.None
})


export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public views: Array<string> = ['Month'];
    public eventSettings: EventSettingsModel = {
        dataSource: scheduleData
    };
    public cssClass: string = 'schedule-date-header-template';
    onRenderCell(args: RenderCellEventArgs): void {
        if (args.elementType === 'monthCells') {
            let ele: Element = document.createElement('div');
            ele.innerHTML = this.getWeather(args.date);
            (args.element).appendChild(ele.firstChild);
        }
    }
    getWeather: Function = (value: Date) => {
        switch (value.getDay()) {
            case 0:
                return '<div class="weather-text">25°C</div>';
            case 1:
                return '<div class="weather-text">18°C</div>';
            case 2:
                return '<div class="weather-text">10°C</div>';
            case 3:
                return '<div class="weather-text">16°C</div>';
            case 4:
                return '<div class="weather-text">8°C</div>';
            case 5:
                return '<div class="weather-text">27°C</div>';
            case 6:
                return '<div class="weather-text">17°C</div>';
            default:
                return null;
        }
    }
}
```

{% endtab %}

> You can refer to our [Angular Scheduler](https://www.syncfusion.com/angular-ui-components/angular-scheduler) feature tour page for its groundbreaking feature representations. You can also explore our [Angular Scheduler example](https://ej2.syncfusion.com/angular/demos/#/material/schedule/overview) to knows how to present and manipulate data.