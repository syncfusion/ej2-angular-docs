---
title: "DocumentEditor web services"
component: "DocumentEditor"
description: "Learn how to create web service in Java for Import, RestrictEditing, Paste with formatting and Spell check."
---

# Creating DocumentEditor web service in Java

DocumentEditor depends on server side interaction for below listed operations can be written in Java using `syncfusion-ej2-wordprocessor-18.1.0.29.jar` file available in [Essential-JS2](https://www.syncfusion.com/downloads/essential-js2) build installed location.

**Syntax:**
> Jar file: `(installed location)/Syncfusion/Essential Studio/JavaScript - EJ2/18.1.0.29/JarFiles/syncfusion-ej2-wordprocessor-18.1.0.29.jar`

**Example:**
> Jar file: `C:/Program Files (x86)/Syncfusion/Essential Studio/JavaScript - EJ2/18.1.0.29/JarFiles/syncfusion-ej2-wordprocessor-18.1.0.29.jar`

* Import Word Document
* Paste with formatting
* Restrict Editing

This section explains how to create the service for DocumentEditor in Java.

## Importing Word Document

Word documents can be imported to DocumentEditor using the below code snippet.

```java
@CrossOrigin(origins = "*", allowedHeaders = "*")
@PostMapping("/api/wordeditor/Import")
public String uploadFile(@RequestParam("files") MultipartFile file) throws Exception {
    try {
        return WordProcessorHelper.load(file.getInputStream(), FormatType.Docx);
    } catch (Exception e) {
        e.printStackTrace();
        return "{\"sections\":[{\"blocks\":[{\"inlines\":[{\"text\":" + e.getMessage() + "}]}]}]}";
    }
}
```

## Paste with formatting

Paste with formatting action is defined in the below code snippet.

```java
@CrossOrigin(origins = "*", allowedHeaders = "*")
@PostMapping("/api/wordeditor/SystemClipboard")
public String systemClipboard(@RequestBody CustomParameter param) {
    if (param.content != null && param.content != "") {
        try {
            return  WordProcessorHelper.loadString(param.content, GetFormatType(param.type.toLowerCase()));
        } catch (Exception e) {
            return "";
        }
    }
    return "";
}

public class CustomParameter {
    public String content;
    public String type;
    public String getContent() {
        return content;
    }
    public String getType() {
        return type;
    }
    public void setContent(String value) {
        content= value;
    }
    public void setType(String value) {
        type = value;
    }
}
```

## Restrict editing

Restrict editing action is defined in the below code snippet.

```java
@CrossOrigin(origins = "*", allowedHeaders = "*")
@PostMapping("/api/wordeditor/RestrictEditing")
public String[] restrictEditing(@RequestBody CustomRestrictParameter param) throws Exception {
    if (param.passwordBase64 == "" && param.passwordBase64 == null)
        return null;
    return WordProcessorHelper.computeHash(param.passwordBase64, param.saltBase64, param.spinCount);
}

public class CustomRestrictParameter {
    public String passwordBase64;
    public String saltBase64;
    public int spinCount;
    public String getPasswordBase64() {
        return passwordBase64;
    }
    public String getSaltBase64() {
        return saltBase64;
    }
    public int getSpinCount() {
        return spinCount;
    }
    public void setPasswordBase64(String value) {
        passwordBase64= value;
    }
    public void setSaltBase64(String value) {
        saltBase64= value;
    }
    public void setSpinCount(int value) {
        spinCount= value;
    }
}
```

>Note: Please refer the [Java Web API sample](https://github.com/SyncfusionExamples/EJ2-DocumentEditor-WebServices/tree/master/Java).