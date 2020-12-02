# Customize ListView as Chat Window

ListView can be customizable as chat window. To achieve that, use ListView [template](../../api/listview#template) property and [Avatar](https://ej2.syncfusion.com/angular/documentation/avatar/getting-started) component.

    * Listview template property is used to showcase the ListView as chat window.
    * Avatar component is used to design the image of contact person.

Refer the below template code snippet for Template of chat window.

```typescript
        <ng-template #template let-data="">
            <div class="settings" *ngIf="data.chat!='receiver' then senderTemplate else receiverTemplate "></div>
            <ng-template #senderTemplate>
                <div id="content">
                    <div class="name">{{data.text}}</div>
                    <div id="info">{{data.contact}}</div>
                </div>
                <div id="image" *ngIf="data.avatar!=''"><span class="e-avatar img1 e-avatar-circle">{{data.avatar}}</span></div>
                <div id="image" *ngIf="data.avatar==''"><span class="{{data.pic}} img1 e-avatar e-avatar-circle"> </span></div>
            </ng-template>

            <ng-template #receiverTemplate>
                <div id="image2" *ngIf="data.avatar!=''"><span class="e-avatar img2 e-avatar-circle">{{data.avatar}}</span></div>
                <div id="image2" *ngIf="data.avatar==''"><span class="{{data.pic}} img2 e-avatar e-avatar-circle"> </span></div>
                <div id="content1">
                    <div class="name1">{{data.text}}</div>
                    <div id="info1">{{data.contact}}</div>
                </div>
            </ng-template>
        </ng-template>
```

## Chat order in template

In ListView template, we have rendered the list items based on receiver and sender information from dataSource of listview.

## Adding messages to chat window

    * Use textbox to get message from user.
    * Add the textbox message to ListView dataSource using [addItem](../../api/listview#additem) method.

```typescript

public btnClick() {
    let value = this.textboxEle.nativeElement.value;
    this.listObj.addItem([{ text: "Amenda", contact: value, id: "2", avatar: "A", pic: "", chat: "receiver" }]);
    this.textboxEle.nativeElement.value = "";
}

```

{% tab template="listview/chat-window", sourceFiles="app/**/*.ts,index.css", isDefaultActive=true %}

```typescript

import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'my-app',
    template: `
    <ejs-listview id='List' #list [dataSource]='data' headerTitle="Chat" showHeader="true" width="350px" [fields]='fields'>
        <ng-template #template let-data="">
            <div class="settings" *ngIf="data.chat!='receiver' then senderTemplate else receiverTemplate "></div>
            <ng-template #senderTemplate>
                <div id="content">
                    <div class="name">{{data.text}}</div>
                    <div id="info">{{data.contact}}</div>
                </div>
                <div id="image" *ngIf="data.avatar!=''"><span class="e-avatar img1 e-avatar-circle">{{data.avatar}}</span></div>
                <div id="image" *ngIf="data.avatar==''"><span class="{{data.pic}} img1 e-avatar e-avatar-circle"> </span></div>
            </ng-template>

            <ng-template #receiverTemplate>
                <div id="image2" *ngIf="data.avatar!=''"><span class="e-avatar img2 e-avatar-circle">{{data.avatar}}</span></div>
                <div id="image2" *ngIf="data.avatar==''"><span class="{{data.pic}} img2 e-avatar e-avatar-circle"> </span></div>
                <div id="content1">
                    <div class="name1">{{data.text}}</div>
                    <div id="info1">{{data.contact}}</div>
                </div>
            </ng-template>
        </ng-template>
    </ejs-listview>
    <div style="width: 350px;margin: 0 auto;"><input #textbox id="name" style="width: 275px" class="e-input" type="text" placeholder="Type your message" />
    <button ejs-button id="btn" style="float:right" (click)="btnClick()">Send</button> </div>
        `,
  })

export class AppComponent {

  @ViewChild('list') listObj: any;
  @ViewChild('textbox') textboxEle: any;
  public data: Object[] = [
    {
      text: "Jenifer",
      contact: "Hi",
      id: "1",
      avatar: "",
      pic: "pic01", chat: "sender"
    },
    { text: "Amenda", contact: "Hello", id: "2", avatar: "A", pic: "", chat: "receiver" },
    {
      text: "Jenifer",
      contact: "What Knid of application going to launch",
      id: "4",
      avatar: "",
      pic: "pic02", chat: "sender"
    },
    {
      text: "Amenda ",
      contact: "A knid of Emergency broadcast App",
      id: "5",
      avatar: "A",
      pic: "", chat: "receiver"
    },
    {
      text: "Jacob",
      contact: "Can you please elaborate",
      id: "6",
      avatar: "",
      pic: "pic04", chat: "sender"
    },
  ];
  public fields = { text: "Name" };

  public btnClick() {
    let value = this.textboxEle.nativeElement.value;
    this.listObj.addItem([{ text: "Amenda", contact: value, id: "2", avatar: "A", pic: "", chat: "receiver" }]);
    this.textboxEle.nativeElement.value = "";
  }
}
```

{% endtab %}
