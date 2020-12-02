---
title: "Autocomplete suggestion"
component: "AutoComplete"
description: "This section explains how to acheive autofill functionality in autocomplete control."
---

# Suggestion list with AutoComplete

The AutoComplete supports to displaying suggestion list upon focusing an empty auto complete component, using the focus event in the control. We have used the filtering and change events to get the typed and selected words and stored them in the browser’s local storage. Then using the focus event, we have displayed the stored list as suggestions.

In the below sample, showcase that how to show `suggestion list` with AutoComplete.

{% tab template="autocomplete/getting-started", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { Query, DataManager, WebApiAdaptor } from '@syncfusion/ej2-data';
import { AutoCompleteComponent, FilteringEventArgs } from '@syncfusion/ej2-angular-dropdowns';

@Component({
  selector: 'app-root',
  template: `<ejs-autocomplete id='country' #local [dataSource]='countries' [fields]='localFields' (change)='onChange()' (filtering)='onFiltering($event)' (focus)='onFocus()'></ejs-autocomplete>`,
})
export class AppComponent {
  @ViewChild('local')
  public localObj: AutoCompleteComponent;
  public suggestList: Array<string> = [];
  public countries: { [key: string]: Object; }[] = [
    { Name: 'Australia', Code: 'AU' },
    { Name: 'Bermuda', Code: 'BM' },
    { Name: 'Canada', Code: 'CA' },
    { Name: 'Cameroon', Code: 'CM' },
    { Name: 'Denmark', Code: 'DK' },
    { Name: 'France', Code: 'FR' },
    { Name: 'Finland', Code: 'FI' }
  ];
  // maps the local data column to fields property
  public localFields: Object = { value: 'Name' };
  onChange() {
    localStorage.setItem("value", this.localObj.value as string);
    if (localStorage.getItem('value') !== 'null') {
      this.suggestList.push(localStorage.getItem('value'));
      var proxy = this;
      this.suggestList = this.suggestList.filter(function (item, pos, self) {
        return proxy.suggestList.indexOf(item) == pos;
      });
    }
  }
  onFocus() {
    if (this.suggestList.length > 0) {
      (this.localObj.dataSource as any) = this.suggestList;
      this.localObj.dataBind();
      let keyEventArgs: any = { preventDefault: (): void => { }, action: 'down', keyCode: 40, type: null };
      (this.localObj as any).onFilterUp(keyEventArgs);
      (this.localObj as any).popupObj.element.classList.add('e-suggestion');
    }
  }
  onFiltering(e: FilteringEventArgs){
    let query: any = new Query();
    query = (e.text !== '') ? query.where('Name', 'startswith', e.text, true) : query;
    e.updateData(this.countries, query);
    (this.localObj as any).popupObj.element.classList.remove('e-suggestion');
        }
}

```

{% endtab %}