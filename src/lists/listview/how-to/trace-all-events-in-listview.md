# Trace all events in ListView

The ListView component triggers events based on its actions. The events can be used as extension points to perform custom operations. Refer to the following steps to trace the ListView events:

1. Render the ListView with [dataSource](../../api/list-view#datasource), and bind the [`actionBegin`](../../api/list-view#actionbegin), [`actionComplete`](../../api/list-view#actioncomplete), and [`select`](../../api/list-view#select) events.

2. Perform custom operations in `actionBegin`, `actionComplete`, and select events.

3. Provide event log details for `actionBegin` and `actionComplete` events, and they will be displayed in the event trace panel when the ListView action starts and the dataSource bound successfully.

4. Get the selected item details from the [`SelectEventArgs`](../../api/list-view/selectEventArgs) in the select event, and display the selected list item text in the event trace panel while selecting list items.

5. Use clear button to remove event trace information.

{% tab template="listview/getting-started", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript

import { Component, ViewChild, ViewEncapsulation } from "@angular/core";
import { SelectEventArgs } from "@syncfusion/ej2-lists";
@Component({
    selector: 'my-app',
    template: `<div id="sample">
      <div class="content-wrapper">
    <ejs-listview id='listview-def' [dataSource]='listData' [width]='250' (select)='onSelect($event)' (actionBegin)='onActionBegin($event)' (actionComplete)='onActionComplete($event)'></ejs-listview>
         </div>
         <div id="list_event">
                <h4><b>Event Trace</b></h4>
                <div id="evt">
                    <div class="eventarea" style="height:273px;overflow: auto">
                        <span #EventLog class="EventLog" id="EventLog" style="word-break: normal;"></span>
                    </div>
                    <div class="evtbtn">
                        <input ejs-button id="clear" type="button" value="Clear" (click)='onclick($event)'>
                    </div>
                </div>
            </div>
        </div>`,
        styles: [`
       #EventLog b {
  color: #388e3c;
}

#listview-def {
  border: 1px solid #dcdcdc;
}
.content-wrapper {
  padding-left: 40px;
  padding-top: 36px;
}

.evtbtn {
  margin-top: 40px;
  margin-left: 70px;
}

/* csslint ignore:start */

hr {
  margin-top: 6px !important;
  margin-bottom: 6px !important;
}

/* csslint ignore:end */

#evt {
  border: 1px solid #dcdcdc;
  padding: 10px;
  min-width: 10px;
}

#sample {
  display: inline-flex;
}

.eventarea {
  min-width: 250px;
}

#list_event {
  margin-top: -25px;
  padding-left:40px;
  min-width: 200px;
}
        `],
        encapsulation: ViewEncapsulation.None
})

export class AppComponent {
    @ViewChild('EventLog') EventLogEle:any;
    public listData: Object =  [
  { text: "Hennessey Venom", id: "list-01" },
  { text: "Bugatti Chiron", id: "list-02" },
  { text: "Bugatti Veyron Super Sport", id: "list-03" },
  { text: "SSC Ultimate Aero", id: "list-04" },
  { text: "Koenigsegg CCR", id: "list-05" },
  { text: "McLaren F1", id: "list-06" },
  { text: "Aston Martin One- 77", id: "list-07" },
  { text: "Jaguar XJ220", id: "list-08" },
  { text: "McLaren P1", id: "list-09" },
  { text: "Ferrari LaFerrari", id: "list-10" }
];
   onclick(event){
    this.EventLogEle.nativeElement.innerHTML = "";
   }
   onSelect(args: SelectEventArgs){
    this.appendElement(args.text + "<b>&nbsp;&nbsp;is selected</b><hr>");
   }
   onActionBegin(){
     this.appendElement("<b>actionBegin </b> event is triggered<hr>");
   }
   onActionComplete(){
     this.appendElement("<b>actionComplete</b> is triggered <hr>");
   }
  appendElement(html: string): void {
     let span: HTMLElement = document.createElement("span");
     span.innerHTML = html;
     let log: HTMLElement = this.EventLogEle.nativeElement;
     log.insertBefore(span, log.firstChild);
}
}

```

{% endtab %}
