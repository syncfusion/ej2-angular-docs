# Display spinner until list items are loaded

The features of the ListView component such as remote data-binding take more time to fetch data from corresponding dataSource/remote URL. In this case, you can use EJ2 [Spinner](https://ej2.syncfusion.com/angular/documentation/spinner/) to enhance the appearance of the UI. This section explains how to load a spinner component to groom the appearance.

Refer to the following code sample to render the spinner component.

```typescript
    createSpinner({
        target: this.spinnerEle.nativeElement
    });
    showSpinner(this.spinnerEle.nativeElement);
```

Refer to the following code sample to render the ListView component.

```typescript
let listviewInstance: ListView = new ListView({
    //Bind the DataManager instance to the dataSource property
    dataSource= new DataManager({
        url: '//js.syncfusion.com/ejServices/Wcf/Northwind.svc/',
        crossDomain: true
    }),

    //Bind the Query instance to the query property
    query= new Query().from('Products').select('ProductID,ProductName').take(10),

    //Map the appropriate columns to the fields property
    fields= { id: 'ProductID', text: 'ProductName' },

});

//Render the initialized ListView
listviewInstance.appendTo("#element");
```

Here, the data is fetched from `Northwind` Service URL; it takes a few seconds to load the data. To enhance the UI, the spinner component has been rendered initially. After the data is loaded from remote URL, the spinner component will be hidden in ListView [actionComplete](../../api/list-view#actioncomplete) event.

{% tab template="listview/getting-started", sourceFiles="app/**/*.ts,index.css", isDefaultActive=true %}

```typescript

import { Component, ViewChild, ngAfterViewInit, ViewEncapsulation } from "@angular/core";
import { DataManager, Query, ODataV4Adaptor } from '@syncfusion/ej2-data';
import { createSpinner, showSpinner, setSpinner } from '@syncfusion/ej2-angular-popups';

@Component({
    selector: 'my-app',
    template: `
    <ejs-listview id='element' #list [dataSource]='dataSource' [width]='300' [query]='query' [fields]='fields' [showHeader]='true' [headerTitle]='headertitle' (actionComplete)='onActionComplete($event)' >
    </ejs-listview>
       <div #spinner id="spinner" ></div>
      `,
        styles: [`
        #element {
    display: block;
    max-width: 400px;
    min-height: 200px;
    margin: auto;
    border: 1px solid #dddddd;
    border-radius: 3px;
}
        `]
})

export class AppComponent {
    @ViewChild('spinner') spinnerEle:any;
    public dataSource= new DataManager({
        url: '//js.syncfusion.com/ejServices/Wcf/Northwind.svc/',
        crossDomain: true
    });
    public query = new Query().from('Products').select('ProductID,ProductName').take(10);
    public fields: Object = { id: 'ProductID', text: 'ProductName'  };
    public headertitle = 'Product Name';
    ngAfterViewInit(){
    createSpinner({
        target: this.spinnerEle.nativeElement
    });
    showSpinner(this.spinnerEle.nativeElement);
   }
   onActionComplete(){
    this.spinnerEle.nativeElement.style.display = "none";
   }
}

```

{% endtab %}
