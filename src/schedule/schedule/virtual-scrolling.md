---
title: "Virtual scrolling in Angular Scheduler"
component: "Scheduler"
description: "This section demonstrtes how to dynamically load the resources and events as you scroll through the scheduler"
---

# Virtual scrolling

To achieve better performance in the Scheduler when loading a large number of resources and events, we have added virtual scrolling support in the timeline views to load a large set of resources and events instantly as you scroll. You can dynamically load large number of resources and events in timeline view of the Scheduler by setting `true` to the `allowVirtualScrolling` property within the timeline view-specific settings. The virtual loading of events is possible in Agenda view, by setting `allowVirtualScrolling` property to `true` within the agenda view specific settings.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, TimelineMonthService, GroupModel } from '@syncfusion/ej2-angular-schedule';

@Component({
  selector: 'app-root',
  providers: [TimelineMonthService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' cssClass='virtual-scrolling' height='550px' [group]="group" [selectedDate]="selectedDate" [eventSettings]="eventSettings">
      <e-resources>
        <e-resource field='ResourceId' title='Resource' [dataSource]='resourceDataSource' [allowMultiple]='allowMultiple'
          name='Resources' textField='Text' idField='Id' colorField='Color'>
        </e-resource>
      </e-resources>
      <e-views>
        <e-view option="TimelineMonth" [allowVirtualScrolling]="virtualscroll"></e-view>
      </e-views>
    </ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 4, 1);
    public group: GroupModel = { byGroupID: false, resources: ['Resources'] };
    public allowMultiple: boolean = true;
    public resourceDataSource: Object[] = this.generateResourceData(1, 300, 'Resource');
    public eventSettings: EventSettingsModel = { dataSource: this.generateStaticEvents(new Date(2018, 4, 1), 300, 12) };
    public virtualscroll: boolean = true;
    private generateStaticEvents(start: Date, resCount: number, overlapCount: number): Object[] {
        let data: Object[] = [];
        let id: number = 1;
        for (let i: number = 0; i < resCount; i++) {
            let randomCollection: number[] = [];
            let random: number = 0;
            for (let j: number = 0; j < overlapCount; j++) {
                random = Math.floor(Math.random() * (30));
                random = (random === 0) ? 1 : random;
                if (randomCollection.indexOf(random) !== -1 || randomCollection.indexOf(random + 2) !== -1 ||
                    randomCollection.indexOf(random - 2) !== -1) {
                    random += (Math.max.apply(null, randomCollection) + 10);
                }
                for (let k: number = 1; k <= 2; k++) {
                    randomCollection.push(random + k);
                }
                let startDate: Date = new Date(start.getFullYear(), start.getMonth(), random);
                startDate = new Date(startDate.getTime() + (((random % 10) * 10) * (1000 * 60)));
                let endDate: Date = new Date(startDate.getTime() + ((1440 + 30) * (1000 * 60)));
                data.push({
                    Id: id,
                    Subject: 'Event #' + id,
                    StartTime: startDate,
                    EndTime: endDate,
                    IsAllDay: (id % 10) ? false : true,
                    ResourceId: i + 1
                });
                id++;
            }
        }
        return data;
    };
    private generateResourceData(startId: number, endId: number, text: string): Object[] {
        let data: { [key: string]: Object }[] = [];
        let colors: string[] = [
            '#ff8787', '#9775fa', '#748ffc', '#3bc9db', '#69db7c',
            '#fdd835', '#748ffc', '#9775fa', '#df5286', '#7fa900',
            '#fec200', '#5978ee', '#00bdae', '#ea80fc'
        ];
        for (let a: number = startId; a <= endId; a++) {
            let n: number = Math.floor(Math.random() * colors.length);
            data.push({
                Id: a,
                Text: text + ' ' + a,
                Color: colors[n]
            });
        }
        return data;
    }
}
```

{% endtab %}

> For now, the virtual loading of resources and events is available only for timeline views. In the future, we plan to port the same virtual loading on all other applicable Scheduler views.

## See Also

* [Virtual scrolling in Agenda view](./views/#agenda-view)