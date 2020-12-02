---
title: "Scrolling"
component: "DocumentEditor"
description: "Learn scrolling and zooming can be customized in JavaScript document editor."
---

# Scrolling

The Document editor renders the document as page by page. You can scroll through the pages by mouse wheel or touch interactions. You can also scroll through the page by using ‘scrollToPage()’ method of document editor instance. Refer to the following code example.

{% tab template="document-editor/find-replace",isDefaultActive=false, sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import {
    DocumentEditorComponent
} from '@syncfusion/ej2-angular-documenteditor';

@Component({
    selector: 'app-container',
    template: `<div style="width:100%;height:330px">
    <ejs-documenteditor #document_editor style="width:100%;height:100%;display:block" (created)="onCreated()"></ejs-documenteditor>
    </div>`,
    encapsulation: ViewEncapsulation.None
})

export class AppComponent {
    @ViewChild('document_editor')
    public documentEditor: DocumentEditorComponent;
    onCreated(): void {
        if (this.documentEditor.isDocumentLoaded) {
            let sfdt: string = {
                "sections": [
                    {
                        "blocks": [
                            {
                                "paragraphFormat": {
                                    "styleName": "Normal"
                                },
                                "inlines": [
                                    {
                                        "text": "First page"
                                    }
                                ]
                            }
                        ],
                        "headersFooters": {},
                    },
                    {
                        "blocks": [
                            {
                                "paragraphFormat": {
                                    "styleName": "Normal"
                                },
                                "inlines": [
                                    {
                                        "text": "Second page"
                                    }
                                ]
                            }
                        ],
                        "headersFooters": {},
                    }
                ],
                "characterFormat": {},
                "paragraphFormat": {},
                "background": {
                    "color": "#FFFFFFFF"
                },
                "styles": [
                    {
                        "type": "Paragraph",
                        "name": "Normal",
                        "next": "Normal"
                    },
                    {
                        "type": "Character",
                        "name": "Default Paragraph Font"
                    }
                ]
            };

            this.documentEditor.open(JSON.stringify(sfdt));
            this.documentEditor.scrollToPage(2);
        }
    }
}

```

{% endtab %}

> Calling this method brings the specified page into view but doesn’t move selection. Hence this method will work by default. That is, it works even if selection is not enabled.

In case, if you wish to move the selection to any page in document editor and bring it into view, you can use ‘goToPage()’ method of selection instance. Refer to the following code example.

{% tab template="document-editor/find-replace",isDefaultActive=false, sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import {
    DocumentEditorComponent, SelectionService
} from '@syncfusion/ej2-angular-documenteditor';

@Component({
    selector: 'app-container',
    template: `<div style="width:100%;height:330px">
    <ejs-documenteditor #document_editor style="width:100%;height:100%;display:block" [enableSelection]=true (created)="onCreated()"></ejs-documenteditor>
    </div>`,
    encapsulation: ViewEncapsulation.None,
    providers: [SelectionService]
})

export class AppComponent {
    @ViewChild('document_editor')
    public documentEditor: DocumentEditorComponent;
    onCreated(): void {
        if (this.documentEditor.isDocumentLoaded) {
            let sfdt: string = {
                "sections": [
                    {
                        "blocks": [
                            {
                                "paragraphFormat": {
                                    "styleName": "Normal"
                                },
                                "inlines": [
                                    {
                                        "text": "First page"
                                    }
                                ]
                            }
                        ],
                        "headersFooters": {},
                    },
                    {
                        "blocks": [
                            {
                                "paragraphFormat": {
                                    "styleName": "Normal"
                                },
                                "inlines": [
                                    {
                                        "text": "Second page"
                                    }
                                ]
                            }
                        ],
                        "headersFooters": {},
                    }
                ],
                "characterFormat": {},
                "paragraphFormat": {},
                "background": {
                    "color": "#FFFFFFFF"
                },
                "styles": [
                    {
                        "type": "Paragraph",
                        "name": "Normal",
                        "next": "Normal"
                    },
                    {
                        "type": "Character",
                        "name": "Default Paragraph Font"
                    }
                ]
            };

            this.documentEditor.open(JSON.stringify(sfdt));
            this.documentEditor.selection.goToPage(2);
        }
    }
}

```

{% endtab %}

## Zooming

You can scale the contents in document editor ranging from 10% to 500% of the actual size. You can achieve this using mouse or touch interactions. You can also use `zoomFactor` property of document editor instance. The value can be specified in a range from 0.1 to 5. Refer to the following code example.

```typescript
this.documentEditor.zoomFactor = 3;
```

## Page Fit Type

Apart from specifying the zoom factor as value, the Document editor provides option to specify page fit options such as fit to full page or fit to page width. You can set this option using ‘fitPage’ method of document editor instance. Refer to the following code example.

```typescript
this.documentEditor.fitPage('Fit page width');
```

## Zoom option using UI

The following code example shows how to provide zoom options in document editor.

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import {
    DocumentEditorComponent
} from '@syncfusion/ej2-angular-documenteditor';

@Component({
    selector: 'app-container',
    template: `<div style="width:100%;height:330px">
     <ejs-documenteditor #documenteditor_editor (selectionChange)='onSelectionChange()' (viewChange)='onViewChange($event)' (documentChange)='onDocumentChange()' (created)="onCreated()" [enableSelection]=true [isReadOnly]=false style="width: 100%;height: 100%;"></ejs-documenteditor>
    </div>
    <div id="documenteditor_statusbar">
        <label style="margin-top: 6px;margin-right: 2px">Page </label>
        <div class="single-line e-de-pagenumber-text" (keydown)='pageKeydownEvent($event)' (click)='pagerClickEvent($event)' id="editablePageNumber" style="font-size:12px;font-weight: 700;display: inline-flex;height: 17px;padding: 0px 4px;" contenteditable="false">
            <label id="documenteditor_page_no" style="text-transform:capitalize;white-space:pre;overflow:hidden;user-select:none;cursor:text;height:17px;max-width:150px">{{currentPage}}</label>
        </div>
        <label id="documenteditor_pagecount_separator" style="margin-left:2px;letter-spacing: 1.05px">of</label>
        <label id="documenteditor_pagecount" style="margin-left:6px;letter-spacing: 1.05px">{{pageCount}}</label>
        <button ejs-dropdownbutton class="e-de-statusbar-zoom" [items]="zoomItems" [content]="zoomContent" (select)="onZoom($event)" iconCss="e-ddb-icons e-profile"></button>
    </div>
    `,
    encapsulation: ViewEncapsulation.None
})

export class AppComponent {
    @ViewChild('document_editor')
    public documentEditor: DocumentEditorComponent;
    public zoomContent: string = "100%";
    public zoomItems = [
        {
            text: '150%',
        },
        {
            text: '125%',
        },
        {
            text: '100%',
        },
        {
            text: '75%',
        },
        {
            text: '50%',
        },
        {
            separator: true
        },
        {
            text: 'Fit one page'
        },
        {
            text: 'Fit page width',
        }];
    public pageCount: number = 1;
    public currentPage: number = 1;

  onCreated(): void {
        if (this.documentEditor.isDocumentLoaded) {
            let sfdt: string = {
            "sections": [
                {
                    "blocks": [
                        {
                            "paragraphFormat": {
                                "styleName": "Normal"
                            },
                            "inlines": [
                                {
                                    "text": "First page"
                                }
                            ]
                        }
                    ],
                    "headersFooters": {},
                },
                {
                    "blocks": [
                        {
                            "paragraphFormat": {
                                "styleName": "Normal"
                            },
                            "inlines": [
                                {
                                    "text": "Second page"
                                }
                            ]
                        }
                    ],
                    "headersFooters": {},
                },
                {
                    "blocks": [
                        {
                            "paragraphFormat": {
                                "styleName": "Normal"
                            },
                            "inlines": [
                                {
                                    "text": "Third page"
                                }
                            ]
                        }
                    ],
                    "headersFooters": {},
                }
            ],
            "characterFormat": {},
            "paragraphFormat": {},
            "background": {
                "color": "#FFFFFFFF"
            },
            "styles": [
                {
                    "type": "Paragraph",
                    "name": "Normal",
                    "next": "Normal"
                },
                {
                    "type": "Character",
                    "name": "Default Paragraph Font"
                }
            ]
        };

            this.documentEditor.open(JSON.stringify(sfdt));
        }
    }

    public onViewChange(args: any) {
        this.currentPage = args.startPage;
    }
    public onSelectionChange(args: any) {
        this.currentPage = this.documentEditor.selection.startPage;
    }
    public onDocumentChange() {
        this.pageCount = this.documentEditor.pageCount
        this.zoomContent = Math.round(this.documentEditor.zoomFactor * 100) + '%';
    }
    public onZoom(args: any) {
        let zoomValue = args.item.text;
        if (zoomValue.match('Fit one page')) {
            this.documentEditor.fitPage('FitOnePage');
        } else if (zoomValue.match('Fit page width')) {
            this.documentEditor.fitPage('FitPageWidth');
        } else {
            this.documentEditor.zoomFactor = parseInt(zoomValue, 0) / 100;
        }
        this.zoomContent = Math.round(this.documentEditor.zoomFactor * 100) + '%';
    }
    public pageKeydownEvent(e: any) {
        if (e.which === 13) {
            e.preventDefault();
            let pageNumber = parseInt(document.getElementById("editablePageNumber").textContent, 0);
            if (pageNumber > this.documentEditor.pageCount) {
                this.updatePageNumber();
            } else {
                this.documentEditor.selection.goToPage(parseInt(document.getElementById("editablePageNumber").textContent, 0));
            }
            document.getElementById("editablePageNumber").contentEditable = 'false';
            if (document.getElementById("editablePageNumber").textContent === '') {
                this.updatePageNumber();
            }
        }
        if (e.which > 64) {
            e.preventDefault();
        }
    }
    public pageBlurEvent() {
        if (document.getElementById("editablePageNumber").textContent === '' || parseInt(document.getElementById("editablePageNumber").textContent, 0) > this.documentEditor.pageCountt) {
            this.updatePageNumber();
        }
        document.getElementById("editablePageNumber").contentEditable = 'false';
    }
    public pagerClickEvent() {
        document.getElementById("editablePageNumber").contentEditable = 'true';
        document.getElementById("editablePageNumber").focus();
        window.getSelection().selectAllChildren(document.getElementById("editablePageNumber"));
    }
    public updatePageNumber() {
        this.currentPage = this.documentEditor.selection.startPage.toString();
    }
}

```