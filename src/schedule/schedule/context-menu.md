---
title: "Context Menu | Angular Scheduler"
component: "Scheduler"
description: "This section explains how to integrate the context menu manually to a Scheduler and use it with required options."
---

# Context menu

You can display context menu on work cells and appointments of Scheduler by making use of the `ContextMenu` control manually from the application end. In the following code example, context menu control is being added from sample end and set its target as `Scheduler`.

On Scheduler cells, you can display the menu items such as `New Event`, `New Recurring Event` and `Today` option. For appointments, you can display its related options such as `Edit Event` and `Delete Event`. The default event window can be opened for appointment creation and editing using the `openEditor` method of Scheduler.

The deletion of appointments can be done by using the `deleteEvent` public method. Also, the `selectedDate` property can be used to navigate between different dates.

> You can also display custom menu options on Scheduler cells and appointments. Context menu will open on tap-hold in responsive mode.

{% tab template="schedule/context-menu", sourceFiles="app/**/*.ts,app/app.component.html", iframeHeight="588px" %}

```typescript
import { Component, ViewChild, ViewEncapsulation } from '@angular/core';
import { extend, closest, isNullOrUndefined, remove, removeClass } from '@syncfusion/ej2-base';
import { DataManager, Query } from '@syncfusion/ej2-data';
import {
    EventSettingsModel, DayService, WeekService, WorkWeekService, MonthService, AgendaService, ScheduleComponent, CellClickEventArgs
} from '@syncfusion/ej2-angular-schedule';
import { ContextMenuComponent, MenuItemModel, BeforeOpenCloseMenuEventArgs, MenuEventArgs } from '@syncfusion/ej2-angular-navigations';
import { scheduleData } from './datasource';

@Component({
    selector: 'app-root',
    templateUrl: 'app/app.component.html',
    providers: [DayService, WeekService, WorkWeekService, MonthService, AgendaService],
    styleUrls: ['app/index.css'],
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild('scheduleObj')
    public scheduleObj: ScheduleComponent;
    @ViewChild('menuObj')
    public menuObj: ContextMenuComponent;
    public allowResizing: Boolean = false;
    public allowDragDrop: Boolean = false;
    public selectedDate: Date = new Date(2018, 1, 15);
    public eventSettings: EventSettingsModel = { dataSource: <Object[]>extend([], scheduleData, null, true) };
    public selectedTarget: Element;
    public menuItems: MenuItemModel[] = [
        {
            text: 'New Event',
            iconCss: 'e-icons new',
            id: 'Add'
        }, {
            text: 'New Recurring Event',
            iconCss: 'e-icons recurrence',
            id: 'AddRecurrence'
        }, {
            text: 'Today',
            iconCss: 'e-icons today',
            id: 'Today'
        }, {
            text: 'Edit Event',
            iconCss: 'e-icons edit',
            id: 'Save'
        }, {
            text: 'Edit Event',
            id: 'EditRecurrenceEvent',
            iconCss: 'e-icons edit',
            items: [{
                text: 'Edit Occurrence',
                id: 'EditOccurrence'
            }, {
                text: 'Edit Series',
                id: 'EditSeries'
            }]
        }, {
            text: 'Delete Event',
            iconCss: 'e-icons delete',
            id: 'Delete'
        }, {
            text: 'Delete Event',
            id: 'DeleteRecurrenceEvent',
            iconCss: 'e-icons delete',
            items: [{
                text: 'Delete Occurrence',
                id: 'DeleteOccurrence'
            }, {
                text: 'Delete Series',
                id: 'DeleteSeries'
            }]
        }
    ];

    onContextMenuBeforeOpen(args: BeforeOpenCloseMenuEventArgs): void {
        const newEventElement: HTMLElement = document.querySelector('.e-new-event') as HTMLElement;
        if (newEventElement) {
            remove(newEventElement);
            removeClass([document.querySelector('.e-selected-cell')], 'e-selected-cell');
        }
        const targetElement: HTMLElement = <HTMLElement>args.event.target;
        if (closest(targetElement, '.e-contextmenu')) {
            return;
        }
        this.selectedTarget = closest(targetElement, '.e-appointment,.e-work-cells,' +
            '.e-vertical-view .e-date-header-wrap .e-all-day-cells,.e-vertical-view .e-date-header-wrap .e-header-cells');
        if (isNullOrUndefined(this.selectedTarget)) {
            args.cancel = true;
            return;
        }
        if (this.selectedTarget.classList.contains('e-appointment')) {
            const eventObj: { [key: string]: Object } = <{ [key: string]: Object }>this.scheduleObj.getEventDetails(this.selectedTarget);
            if (eventObj.RecurrenceRule) {
                this.menuObj.showItems(['EditRecurrenceEvent', 'DeleteRecurrenceEvent'], true);
                this.menuObj.hideItems(['Add', 'AddRecurrence', 'Today', 'Save', 'Delete'], true);
            } else {
                this.menuObj.showItems(['Save', 'Delete'], true);
                this.menuObj.hideItems(['Add', 'AddRecurrence', 'Today', 'EditRecurrenceEvent', 'DeleteRecurrenceEvent'], true);
            }
            return;
        }
        this.menuObj.hideItems(['Save', 'Delete', 'EditRecurrenceEvent', 'DeleteRecurrenceEvent'], true);
        this.menuObj.showItems(['Add', 'AddRecurrence', 'Today'], true);
    }

    onMenuItemSelect(args: MenuEventArgs): void {
        const selectedMenuItem: string = args.item.id;
        let eventObj: { [key: string]: Object };
        if (this.selectedTarget && this.selectedTarget.classList.contains('e-appointment')) {
            eventObj = <{ [key: string]: Object }>this.scheduleObj.getEventDetails(this.selectedTarget);
        }
        switch (selectedMenuItem) {
            case 'Today':
                this.scheduleObj.selectedDate = new Date();
                break;
            case 'Add':
            case 'AddRecurrence':
                const selectedCells: Element[] = this.scheduleObj.getSelectedElements();
                const activeCellsData: CellClickEventArgs = this.scheduleObj.getCellDetails(selectedCells.length > 0 ? selectedCells : selectedTarget);
                if (selectedMenuItem === 'Add') {
                    this.scheduleObj.openEditor(activeCellsData, 'Add');
                } else {
                    this.scheduleObj.openEditor(activeCellsData, 'Add', null, 1);
                }
                break;
            case 'Save':
            case 'EditOccurrence':
            case 'EditSeries':
                if (selectedMenuItem === 'EditSeries') {
                    eventObj = <{ [key: string]: Object }>new DataManager(this.scheduleObj.eventsData).executeLocal(new Query().
                        where(this.scheduleObj.eventFields.id, 'equal', eventObj[this.scheduleObj.eventFields.recurrenceID] as string | number))[0];
                }
                this.scheduleObj.openEditor(eventObj, selectedMenuItem);
                break;
            case 'Delete':
                this.scheduleObj.deleteEvent(eventObj);
                break;
            case 'DeleteOccurrence':
            case 'DeleteSeries':
                this.scheduleObj.deleteEvent(eventObj, selectedMenuItem);
                break;
        }
    }
}
```

{% endtab %}
