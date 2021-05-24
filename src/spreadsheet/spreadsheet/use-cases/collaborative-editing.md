---
title: "Collaborative Editing in Spreadsheet"
component: "Spreadsheet"
description: "This section helps to learn how to collaborative editing in Spreadsheet control"
---

# Collaborative Editing

The collaborative editing support allows you to work at a spreadsheet collaboratively with other users. Multiple users can access to the the same spreadsheet simultaneously.

> * To use Collaborative editing, inject the `CollaborativeEditing` module in the spreadsheet.

## Dependencies

The following list of dependencies are required to use the collaborative editing support in spreadsheet.

```js
|-- @aspnet/signalr
   |-- eventsource
   |-- request
   |-- ws

```

> * Run the command `npm i @aspnet/signalr` to install `@aspnet/signalr` packages in your application.

## Client configuration

To broadcast the data for every action is spreadsheet, you need to transfer the data to the server through `send` method in `actionComplete` event and receive the same data by using the `dataReceived` method. In the `dataReceived` method, you need to update the action to the connected clients through `updateAction` method.

The following code example shows `Collaborative Editing` support in the Spreadsheet control.

```javascript
import { Component, ViewChild } from '@angular/core';
import { SpreadsheetComponent } from '@syncfusion/ej2-angular-spreadsheet';
import { Spreadsheet } from '@syncfusion/ej2-spreadsheet';
import { defaultData } from './datasource';
import * as signalR from '@aspnet/signalr';
import { HubConnection, HubConnectionBuilder } from '@aspnet/signalr';

@Component({
    selector: 'app-container',
    template: `<ejs-spreadsheet #spreadsheet (actionComplete)="onActionComplete()">
                <e-sheets>
                  <e-sheet>
                    <e-ranges>
                      <e-range [dataSource]="data"></e-range>
                    </e-ranges>
                    <e-columns>
                      <e-column [width]=180></e-column>
                      <e-column [width]=130></e-column>
                      <e-column [width]=130></e-column>
                    </e-columns>
                  </e-sheet>
                </e-sheets>
              </ejs-spreadsheet>`
})
export class AppComponent {
    @ViewChild('spreadsheet')
    spreadsheetObj: SpreadsheetComponent;
    connection: HubConnection;
    data: object[] = defaultData;
    ngOnInit(): void {
      // For signalR Hub connection
      this.connection  = new HubConnectionBuilder()  
      .withUrl('https://localhost:44385/hubs/spreadsheethub', {  // localhost from AspNetCore service
        skipNegotiation: true,
        transport: signalR.HttpTransportType.WebSockets
      })  
      .build();

        this.connection.on('dataReceived', (data: string) => {
          var model = JSON.parse(data);
          this.spreadsheetObj.updateAction({ action: model.action, eventArgs: model.eventArgs }); // update the action to the connected clients
      });
  
      this.connection.start().then(() => { // to start the server
             console.log('server connected!!!');
         }).catch(err => console.log(err));
  }
    onActionComplete(args:any) {
        this.connection.send('BroadcastData', JSON.stringify(args)); // send the action data to the server
    }
}
```

## Server configuration

To make the communication between the server to the connected clients and from clients to the server, you need to configure the signalR Hubs using the following code.

```js
import * as signalR from '@aspnet/signalr';

// For signalR Hub connection
    public connection = new signalR.HubConnectionBuilder().withUrl('https://localhost:44385/hubs/spreadsheethub', { // localhost from AspNetCore service
        skipNegotiation: true,
        transport: signalR.HttpTransportType.WebSockets
    }).build();
```

## Hub configuration

Initially create a AspNetCore project and add the hub file for sending and receiving the data between server and clients.

```javascipt
using Microsoft.AspNetCore.SignalR;
using System.Threading.Tasks;

namespace WebApplication.Hubs
{
    public class SpreadsheetHub : Hub
    {
        public async Task BroadcastData(string data)
        {
            await Clients.All.SendAsync("dataReceived", data);
        }
    }
}
```

To configure the SignalR middleware by registering the following service in the `ConfigureServices` method of the `Startup` class.

```javascipt
    services.AddSignalR();
```

To set up the SignalR routes by calling MapHub in the `Configure` method of the `Startup` class.

```javascipt

    app.UseEndpoints(endpoints =>

    {

        endpoints.MapRazorPages();

        endpoints.MapHub<SpreadsheetHub>("/spreadsheetHub");

    });
```

For hosting the service, you may use the above code snippet or download and run the [local service](https://www.syncfusion.com/downloads/support/directtrac/general/ze/WebApplication1377017438).

## Prevent the particular action update for collaborative client

Using the `action` argument from the `actionComplete` event, you can prevent the particular action update for collaborative client.

The following code example shows how to prevent collaborative client from updating the `format` action.

```javascript
import { Component, ViewChild } from '@angular/core';
import { SpreadsheetComponent } from '@syncfusion/ej2-angular-spreadsheet';
import { defaultData } from './datasource';
import * as signalR from '@aspnet/signalr';
import { HubConnection, HubConnectionBuilder } from '@aspnet/signalr';

@Component({
    selector: 'app-container',
    template: `<ejs-spreadsheet #spreadsheet (actionComplete)="onActionComplete()">
                <e-sheets>
                  <e-sheet>
                    <e-ranges>
                      <e-range [dataSource]="data"></e-range>
                    </e-ranges>
                    <e-columns>
                      <e-column [width]=180></e-column>
                      <e-column [width]=130></e-column>
                      <e-column [width]=130></e-column>
                    </e-columns>
                  </e-sheet>
                </e-sheets>
              </ejs-spreadsheet>`
})
export class AppComponent {
    @ViewChild('spreadsheet')
    spreadsheetObj: SpreadsheetComponent;
    data: object[] = defaultData;
    // For signalR Hub connection
    public connection = new signalR.HubConnectionBuilder().withUrl('https://localhost:44385/hubs/spreadsheethub', { // localhost from AspNetCore service
        skipNegotiation: true,
        transport: signalR.HttpTransportType.WebSockets
    }).build();

    ngOnInit(): void {
        this.connection.on('dataReceived', (data: string) => {
            var model = JSON.parse(data);
            this.spreadsheetObj.updateAction({ action: model.action, eventArgs: model.eventArgs }); // update the action to the connected clients
        });
        this.connection.start().then(() => { // to start the server
            console.log('server connected!!!');
        }).catch(err => console.log(err));
    }
    onActionComplete(args) {
        if (args.action != 'format'){
          this.connection.send('BroadcastData', JSON.stringify(args)); // send the action data to the server
        }
    }
}
```
