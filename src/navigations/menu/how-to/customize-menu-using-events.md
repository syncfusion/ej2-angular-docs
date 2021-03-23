# Customize menu using events

The Menu provides a set of [`events`](../api/menu#events) to enable users to customize it.

The available events are [`beforeOpen`](../../api/menu/#beforeclose), [`beforeClose`](../..api//menu/#beforeopen), [`onClose`](../../api/menu/#onclose), [`onOpen`](../../api/menu/#onopen), and [`select`](../..api//menu/#select).

{% tab template="menu/handle-event", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { enableRipple } from '@syncfusion/ej2-base';
import { MenuItemModel, OpenCloseMenuEventArgs, BeforeOpenCloseMenuEventArgs, MenuEventArgs } from '@syncfusion/ej2-angular-navigations';

enableRipple(true);

@Component({
selector: 'app-root',
template: `<div class="control-section">
    <div class="menu-section">
        <ejs-menu id='menu' [items]='menuItems' (beforeOpen)='beforeOpen($event)' (beforeClose)='beforeClose($event)' (onClose)='onClose($event)' (onOpen)='onOpen($event)' (select)='select($event)'></ejs-menu>
    </div>
    <div class="property-section">
        <table id="propertyTable" title="Event trace">
            <tbody>
                <th>Event trace:-</th>
                <tr>
                <td [innerHTML]="eventTrace"></td>
                </tr>
            </tbody>
        </table>
    </div>
    <button id='clear' ejs-button cssClass='e-small' (click)='btnClick()'>Clear</button>
    </div>`
})

export class AppComponent {
    private eventTrace: string = '';
    private menuItems: MenuItemModel[] = [
        {
            text: 'Events',
            items: [
                { text: 'Conferences' },
                { text: 'Music' },
                { text: 'Workshops' }
            ]
        },
        {
            text: 'Movies',
            items: [
                { text: 'Now Showing' },
                { text: 'Coming Soon' }
            ]
        },
        {
            text: 'Directory',
            items: [
                { text: 'Media Gallery' },
                { text: 'Newsletters' }
            ]
        },
        {
            text: 'Queries',
            items: [
                { text: 'Our Policy' },
                { text: 'Site Map' }
            ]
        },
        { text: 'Services' }
    ];

    private beforeOpen(args: BeforeOpenCloseMenuEventArgs): void {
        this.updateEventLog(args);
    }

    private beforeClose(args: BeforeOpenCloseMenuEventArgs): void {
        this.updateEventLog(args);
    }

    private onClose(args: OpenCloseMenuEventArgs): void {
        this.updateEventLog(args);
    }

    private onOpen(args: OpenCloseMenuEventArgs): void {
        this.updateEventLog(args);
    }

    private select(args: MenuEventArgs): void {
        this.updateEventLog(args);
    }

    private updateEventLog(args: any): void {
        this.eventTrace = this.eventTrace + args.name + ' Event triggered. <br />'
    }

    private btnClick(): void {
        this.eventTrace = '';
    }
}
```

{% endtab %}
