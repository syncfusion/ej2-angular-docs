---
title: "File Manager Localization"
component: "File Manager"
description: "Localization support in File Manager"
---

# Localization

The file manager can be localized to any culture by defining the texts and messages of the file manager in the corresponding culture. The default locale of the file manager is `en`(English). The following table represents the default texts and messages of the file manager in `en` culture.

|KEY|Text/Message|
|----|----|
|NewFolder|New folder|
|Upload|Upload|
|Delete|Delete|
|Rename|Rename|
|Download|Download|
|Cut|Cut|
|Copy|Copy|
|Paste|Paste|
|SortBy|Sort by|
|Refresh|Refresh|
|Item-Selection|item selected|
|Items-Selection|items selected|
|View|View|
|Details|Details|
|SelectAll|Select all|
|Open|Open|
|Tooltip-NewFolder|New folder|
|Tooltip-Upload|Upload|
|Tooltip-Delete|Delete|
|Tooltip-Rename|Rename|
|Tooltip-Download|Download|
|Tooltip-Cut|Cut|
|Tooltip-Copy|Copy|
|Tooltip-Paste|Paste|
|Tooltip-SortBy|Sort by|
|Tooltip-Refresh|Refresh|
|Tooltip-Selection|Clear selection|
|Tooltip-View|View|
|Tooltip-Details|Details|
|Tooltip-SelectAll|Select all|
|Name|Name|
|Size|Size|
|DateModified|Modified|
|DateCreated|Date created|
|Path|Path|
|Created|Created|
|Modified|Modified|
|Location|Location|
|Type|Type|
|Permission|Permission|
|Ascending|Ascending|
|Descending|Descending|
|None|None|
|View-LargeIcons|Large icons|
|View-Details|Details|
|Search|Search|
|Button-Ok|OK|
|Button-Cancel|Cancel|
|Button-Yes|Yes|
|Button-No|No|
|Button-Create|Create|
|Button-Save|Save|
|Header-NewFolder|Folder|
|Content-NewFolder|Enter your folder name|
|Header-Rename|Rename|
|Content-Rename|Enter your new name|
|Header-Rename-Confirmation|Rename Confirmation|
|Content-Rename-Confirmation|If you change a file name extension| the file might become unstable. Are you sure you want to change it?|
|Header-Delete|Delete File|
|Content-Delete|Are you sure you want to delete this file?|
|Header-Multiple-Delete|Delete Multiple Files|
|Content-Multiple-Delete|Are you sure you want to delete these {0} files?|
|Header-Folder-Delete|Delete Folder|
|Content-Folder-Delete|Are you sure you want to delete this folder?|
|Header-Duplicate|File exists|
|Content-Duplicate| already exists. Are you sure you want to replace it?|
|Header-Upload|Upload Files|
|Error|Error|
|Validation-Empty|The file or folder name cannot be empty.|
|Validation-Invalid|The file or folder name {0} contains invalid characters. Please use a different name. Valid file or folder names cannot end with a dot or space, and cannot contain any of the following characters: \\/:*?\"<>\||
|Validation-NewFolder-Exists|A file or folder with the name {0} already exists.|
|Validation-Rename-Exists|Cannot rename {0} to {1}| destination already exists.|
|Folder-Empty|This folder is empty|
|File-Upload|Drag files here to upload|
|Search-Empty|No results found|
|Search-Key|Try with different keywords|
|Filter-Empty|No results found|
|Filter-Key|Try with different filter|
|Sub-Folder-Error|The destination folder is the subfolder of the source folder|
|Access-Denied|Access Denied|
|Access-Details|You don't have permission to access this folder|
|Header-Retry|File Already Exists|
|Content-Retry|A file with this name already exists in this folder. What would you like to do?|
|Button-Keep-Both|Keep both|
|Button-Replace|Replace|
|Button-Skip|Skip|
|ApplyAll-Label|Do this for all current items|
|KB|KB|
|Access-Message|{0} is not accessible. You need permission to perform the {1} action.|
|Network-Error|NetworkError: Failed to send on XMLHTTPRequest: Failed to load|
|Server-Error|ServerError: Invalid response from|

The below example shows adding the German culture locale(`de-DE`)

{% tab template="file-manager/localization", isDefaultActive = "true",sourceFiles="app/**/*.ts,app/app.component.html" %}

```typescript

import { Component } from '@angular/core';
import { L10n } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    styleUrls: ['app/app.component.css'],
    templateUrl: 'app/app.component.html'
})
export class AppComponent {
    public ajaxSettings: object;
    public locale: string;
    public hostUrl: string = 'https://ej2-aspcore-service.azurewebsites.net/';
    public ngOnInit(): void {
    L10n.load({
    'de': {
        'filemanager': {
            "NewFolder": "Neuer Ordner",
            "Upload": "Hochladen",
            "Delete": "Löschen",
            "Rename": "Umbenennen",
            "Download": "Herunterladen",
            "Cut": "Schnitt",
            "Copy": "Kopieren",
            "Paste": "Einfügen",
            "SortBy": "Sortiere nach",
            "Refresh": "Aktualisierung",
            "Item-Selection": "Artikel ausgewählt",
            "Items-Selection": "Elemente ausgewählt",
            "View": "Aussicht",
            "Details": "Einzelheiten",
            "SelectAll": "Wählen Sie Alle",
            "Open": "Öffnen",
            "Tooltip-NewFolder": "Neuer Ordner",
            "Tooltip-Upload": "Hochladen",
            "Tooltip-Delete": "Löschen",
            "Tooltip-Rename": "Umbenennen",
            "Tooltip-Download": "Herunterladen",
            "Tooltip-Cut": "Schnitt",
            "Tooltip-Copy": "Kopieren",
            "Tooltip-Paste": "Einfügen",
            "Tooltip-SortBy": "Sortiere nach",
            "Tooltip-Refresh": "Aktualisierung",
            "Tooltip-Selection": "Auswahl aufheben",
            "Tooltip-View": "Aussicht",
            "Tooltip-Details": "Einzelheiten",
            "Tooltip-SelectAll": "Wählen Sie Alle",
            "Name": "Name",
            "Size": "Größe",
            "DateModified": "Geändert",
            "DateCreated": "Datum erstellt",
            "Path": "Pfad",
            "Modified": "Geändert",
            "Created": "Erstellt",
            "Location": "Ort",
            "Type": "Art",
            "Permission": "Genehmigung",
            "Ascending": "Aufsteigend",
            "Descending": "Absteigend",
            "None": "Keiner",
            "View-LargeIcons": "Große Icons",
            "View-Details": "Einzelheiten",
            "Search": "Suche",
            "Button-Ok": "OK",
            "Button-Cancel": "Stornieren",
            "Button-Yes": "Ja",
            "Button-No": "Nein",
            "Button-Create": "Erstellen",
            "Button-Save": "Sparen",
            "Header-NewFolder": "Mappe",
            "Content-NewFolder": "Geben Sie Ihren Ordnernamen ein",
            "Header-Rename": "Umbenennen",
            "Content-Rename": "Geben Sie Ihren neuen Namen ein",
            "Header-Rename-Confirmation": "Bestätigung umbenennen",
            "Content-Rename-Confirmation": "Wenn Sie eine Dateinamenerweiterung ändern, wird die Datei möglicherweise instabil. Möchten Sie sie wirklich ändern?",
            "Header-Delete": "Datei löschen",
            "Content-Delete": "Möchten Sie diese Datei wirklich löschen?",
            "Header-Multiple-Delete": "Mehrere Dateien löschen",
            "Content-Multiple-Delete": "Möchten Sie diese {0} Dateien wirklich löschen?",
            "Header-Folder-Delete": "Lösche Ordner",
            "Content-Folder-Delete": "Möchten Sie diesen Ordner wirklich löschen?",
            "Header-Duplicate": "Datei / Ordner existiert",
            "Content-Duplicate": "{0} existiert bereits. Möchten Sie umbenennen und einfügen?",
            "Header-Upload": "Daten hochladen",
            "Error": "Error",
            "Validation-Empty": "Der Datei - oder Ordnername darf nicht leer sein.",
            "Validation-Invalid": "Der Datei- oder Ordnername {0} enthält ungültige Zeichen. Bitte verwenden Sie einen anderen Namen. Gültige Datei- oder Ordnernamen dürfen nicht mit einem Punkt oder Leerzeichen enden und keines der folgenden Zeichen enthalten: \\ /: *? \" < > | ",
            "Validation-NewFolder-Exists": "Eine Datei oder ein Ordner mit dem Namen {0} existiert bereits.",
            "Validation-Rename-Exists": "{0} kann nicht in {1} umbenannt werden: Ziel existiert bereits.",
            "Folder-Empty": "Dieser Ordner ist leer",
            "File-Upload": "Dateien zum Hochladen hierher ziehen",
            "Search-Empty": "Keine Ergebnisse gefunden",
            "Search-Key": "Versuchen Sie es mit anderen Stichwörtern",
            "Filter-Empty": "keine Ergebnisse gefunden",
            "Filter-Key" : "Versuchen Sie es mit einem anderen Filter",
            "Sub-Folder-Error": "Der Zielordner ist der Unterordner des Quellordners.",
            "Access-Denied": "Zugriff verweigert",
            "Access-Details": "Sie haben keine Berechtigung, auf diesen Ordner zuzugreifen.",
            "Header-Retry": "Die Datei existiert bereits",
            "Content-Retry": "In diesem Ordner ist bereits eine Datei mit diesem Namen vorhanden. Was möchten Sie tun?",
            "Button-Keep-Both": "Behalte beides",
            "Button-Replace": "Ersetzen",
            "Button-Skip": "Überspringen",
            "ApplyAll-Label": "Mache das für alle aktuellen Artikel",
            "KB": "KB",
            "Access-Message": "{0} ist nicht zugänglich. Sie benötigen die Berechtigung, um die Aktion {1} auszuführen.",
            "Network-Error": "NetworkError: Fehler beim Senden auf XMLHTTPRequest: Fehler beim Laden",
            "Server-Error": "ServerError: Ungültige Antwort von"
        }
    }
    });
    this.ajaxSettings = {
        url: this.hostUrl + 'api/FileManager/FileOperations',
        getImageUrl: this.hostUrl + 'api/FileManager/GetImage',
        uploadUrl: this.hostUrl + 'api/FileManager/Upload',
        downloadUrl: this.hostUrl + 'api/FileManager/Download'
    };
    this.locale =  'de';
    }
}

```

{% endtab %}
