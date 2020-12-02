# Load HTML content via AJAX

We can set external `HTML` page content as [`template`](../../api/list-view#template) for our `ListView` component by making use of `AJAX` call.

```typescript

let ajax = new Ajax('./template.html', 'GET', false);
    ajax.onSuccess = (e)=>{
        this.listtemplate = e;
    };
    ajax.send();

```

In the below sample, we have rendered smartphone settings template from external `HTML` file.

{% tab template="listview/ajax", sourceFiles="app/**/*.ts,index.css", isDefaultActive=true %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { Ajax } from '@syncfusion/ej2-base';

@Component({
    selector: 'my-app',
    template: `
          <ejs-listview id='List' [dataSource]='data' showHeader='true' headerTitle='Settings' [template]="listtemplate">
        </ejs-listview>
        `
})

export class AppComponent {
  public listtemplate;
  public data =  [
    { text: 'Network & Internet', id: '0', description: 'Wi-Fi, mobile, data usage, hotspot' },
    { text: 'Connected devices', id: '1', description: 'Bluetooth, cast, NFC' },
    { text: 'Battery', id: '2', description: '18% -4h 12m left' },
    { text: 'Display', id: '3', description: 'Wallpaper, sleep, font size' },
    { text: 'Sound', id: '4', description: 'Volume, vibration, Do Not Disturb' },
    { text: 'Storage', id: '5', description: '52% used - 15.48 GB free' }
    ];
    ngOnInit(){
        let ajax = new Ajax('./template.html', 'GET', false);
        ajax.onSuccess = (e)=>{
          this.listtemplate = e;
        };
        ajax.send();
    }
}
```

{% endtab %}
