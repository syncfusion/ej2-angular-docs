# Template

## Show table in sub ContextMenu

Menu items of the ContextMenu can be customized according to the requirement. The section
explains about how to customize table template in sub menu item.

This can be achieved by appending table layout while `li` rendering by using `beforeItemRender` event.

{% tab template= "context-menu/table", sourceFiles="app/**/*.ts,styles.css", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { ContextMenu, BeforeOpenCloseMenuEventArgs, MenuEventArgs, MenuItemModel } from '@syncfusion/ej2-navigations';
import { createCheckBox } from '@syncfusion/ej2-buttons';
import { closest } from '@syncfusion/ej2-base';

@Component({
  selector: 'app-root',
  template: `
  <div id="target">Right click / Touch hold to open the ContextMenu</div>
  <ejs-contextmenu id='contextmenu' [target]='target' [items]= 'menuItems' (beforeItemRender)='itemRender($event)'></ejs-contextmenu>`
})

export class AppComponent  {
public target: string = '#target';

public menuItems: MenuItemModel[] = [
{
    text: 'Cut',
    iconCss: 'e-cm-icons e-cut'
},
{
    text: 'Copy',
    iconCss: 'e-cm-icons e-copy'
},
{
    text: 'Paste',
    iconCss: 'e-cm-icons e-paste'
},
{
    separator: true
},
{
    text: 'Link',
    iconCss: 'e-icons e-link'
},
{
    text: 'Table',
    iconCss: 'e-icons e-table',
    items: [
        {
            id: 'table'
        }
    ]
}];

public itemRender(args:MenuEventArgs ) {
   if (args.item.id === 'table') {
     args.element.classList.add('bg-transparent');
     args.element.appendChild(this.createHeader());
     args.element.appendChild(this.createTable());
   }
}

public createHeader() {
  let header: HTMLElement = document.createElement('h4');
  header.textContent = 'Insert Table';
  return header;
}
public createTable() {
    let table: HTMLElement = document.createElement('table');
    for (let i: number = 0; i < 5; i++) {
        let row: HTMLElement = document.createElement('tr');
        table.appendChild(row);
    for (let j: number = 0; j < 6; j++) {
        let col: HTMLElement = document.createElement('td');
        row.appendChild(col);
    col.setAttribute('class', 'e-data');
    }
}
return table;
}
}
```

{% endtab %}

## Show UI components in ContextMenu

UI components can also be placed inside the each `li` element of ContextMenu.

In the following example, CheckBox component is placed inside each `li` element and
this can be achieved by creating CheckBox component in `beforeItemRender` event and
appending it into the `li` element.

{% tab template= "context-menu/how-to", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { BeforeOpenCloseMenuEventArgs, MenuEventArgs, MenuItemModel } from '@syncfusion/ej2-navigations';
import { createCheckBox } from '@syncfusion/ej2-buttons';
import { closest, createElement } from '@syncfusion/ej2-base';

@Component({
  selector: 'app-root',
  template: `
  <div id="target">Right click / Touch hold to open the ContextMenu</div>
  <ejs-contextmenu id='contextmenu' [target]='target' [items]= 'menuItems' (beforeItemRender)='itemRender($event)' (beforeClose)='beforeClose($event)'></ejs-contextmenu>`
})

export class AppComponent  {
   public target: string = '#target';
   public menuItems: MenuItemModel[] = [
    { text: 'Option 1' },
    { text: 'Option 2' },
    { text: 'Option 3' }
   ];

    public beforeClose(args:BeforeOpenCloseMenuEventArgs ) {
        if ((args.event.target as Element).closest('.e-menu-item')) {
            args.cancel = true;
            let selectedElem: NodeList = args.element.querySelectorAll('.e-selected');
            for(let i:number=0; i < selectedElem.length; i++){
                let ele: Element = selectedElem[i] as Element;
                ele.classList.remove('e-selected');
            }
            let checkbox: HTMLElement = closest(args.event.target as Element, '.e-checkbox-wrapper') as HTMLElement;
            let frame: HTMLElement = checkbox.querySelector('.e-frame');
            if (checkbox && frame.classList.contains('e-check')) {
                frame.classList.remove('e-check');
            } else if (checkbox) {
                frame.classList.add('e-check');
            }
        }
    }

    public itemRender(args: MenuEventArgs ) {
        let check: Element = createCheckBox(createElement, false, {
            label: args.item.text,
            checked: (args.item.text == 'Option 2') ? true : false
        });
        args.element.innerHTML = '';
        args.element.appendChild(check);
    }
}
```

{% endtab %}
