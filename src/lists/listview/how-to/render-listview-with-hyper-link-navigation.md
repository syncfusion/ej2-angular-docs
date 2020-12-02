# Render ListView with hyper link navigation

We can use `anchor` tag along with `href` attribute in our ListView [`template`](../../api/list-view#template) property for navigation.

```typescript

<ng-template #template let-data="">
   <a target='_blank' href="{{data.url}}">{{data.name}}</a>
</ng-template>

```

In the below sample, we have rendered `ListView` with search engines URL.

{% tab template="listview/navigation", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript

import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'my-app',
    template: `
          <div id="sample">
    <ejs-listview id='List' [dataSource]='data' headerTitle='Search engines' showHeader='true'>
    <ng-template #template let-data="">
   <a target='_blank' href="{{data.url}}">{{data.name}}</a>
    </ng-template>
    </ejs-listview>
  </div>
        `,
  })

export class AppComponent {

  public data=[
        {name: 'Google', url: 'https://www.google.com'},
        {name: 'Bing', url: 'https://www.bing.com' },
        {name: 'Yahoo', url: 'https://www.yahoo.com'},
        {name: 'Ask.com', url: 'https://www.ask.com'},
        {name: 'AOL.com', url: 'https://www.aol.com'},
    ];

}
```

{% endtab %}
