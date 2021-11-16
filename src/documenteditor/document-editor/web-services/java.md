---
title: "Java web service for Word Processor a.k.a. Document Editor"
component: "DocumentEditor"
description: "Illustrates how to create web service in Java for the server-side dependent functionalities of Word Processor component a.k.a. Document Editor."
---

# Using Java web service in JavaScript DocumentEditor control

This page illustrates how to create web service in Java for the server-side dependent functionalities of Word Processor component a.k.a. Document Editor. Document Editor depends on server side interaction for below listed operations and it can be written in Java using `syncfusion-ej2-wordprocessor.jar` file.

* Import Word Document
* Paste with formatting
* Restrict Editing

## Supported Java versions

Syncfusion Java library supports Java SE 8.0(1.8) or above versions.

## External Jars Required

The following jar files are required to be referenced in your Java application.

1. syncfusion-ej2-wordprocessor

2. syncfusion-docio

3. syncfusion-javahelper

## Download JAR file

The JAR file is available in both [Syncfusion Essential-JS2](https://www.syncfusion.com/downloads/essential-js2) build and maven repository.

### Get JAR file from Syncfusion build

You can get the `syncfusion-ej2-wordprocessor.jar` and its dependent jar files from Syncfusion build installed location.

**Syntax:**
> Jar file: `(installed location)/Syncfusion/Essential Studio/{Platform}/{version}/JarFiles/syncfusion-ej2-wordprocessor-{version}.jar`

**Example:**
> Jar file: `C:/Program Files (x86)/Syncfusion/Essential Studio/JavaScript - EJ2/18.4.0.30/JarFiles/syncfusion-ej2-wordprocessor-18.4.0.30.jar`

You can also get the jar files by installing [file formats controls](https://www.syncfusion.com/sales/products/fileformats?utm_source=ug&utm_medium=listing&utm_campaign=java-word-processor#). You can find the required jars in the build installed location.

**Syntax:**
> Jar file: `(installed location)/Syncfusion/Essential Studio/{Platform}/{version}/JarFiles/syncfusion-ej2-wordprocessor-{version}.jar`

**Example:**
> Jar file: `C:/Program Files (x86)/Syncfusion/Essential Studio/FileFormats/18.4.0.30/JarFiles/syncfusion-ej2-wordprocessor-18.4.0.30.jar`

### Referring JAR from Syncfusion Maven Repository

You can download the jars from the Syncfusion [maven repository](https://jars.syncfusion.com/) to use our artifacts in your projects. It helps to use the Syncfusion Java packages without installing Essential Studio or platform installation to development with Syncfusion controls.

#### Download Syncfusion Java packages

You can easily download the Syncfusion packages for Java via maven repository. Follow the below guidelines to configure as per the tool.

#### Refer the maven repository in build tool

##### Gradle

```java
  repositories {
      maven {
      // Syncfusion maven repository to download the artifacts
      url "https://jars.syncfusion.com/repository/maven-public/"
      }
  }
```

##### Apache Maven

```java
  <repository>
      <id>Syncfusion-Java</id>
      <name>Syncfusion Java repo</name>
      <url>https://jars.syncfusion.com/repository/maven-public/</url>
  </repository>
```

#### Refer the Syncfusion package in your project as the dependency

##### Gradle

```java
  dependencies {
        implementation 'com.syncfusion:syncfusion-ej2-wordprocessor:18.4.0.30'
  }
```

##### Apache Maven

```java
  <dependency>
      <groupId>com.syncfusion</groupId>
      <artifactId>syncfusion-ej2-wordprocessor</artifactId>
      <version>18.4.0.30</version>
  </dependency>
```

This section explains how to create the Java web service for DocumentEditor.

## Importing Word Document

The following code converts the Word document to SFDT file and sends the converted SFDT to client for importing Word document in DocumentEditor.

```java
  @CrossOrigin(origins = "*", allowedHeaders = "*")
  @PostMapping("/api/wordeditor/Import")
  public String uploadFile(@RequestParam("files") MultipartFile file) throws Exception {
        try {
            //Convert the word document into sfdt.
            return WordProcessorHelper.load(file.getInputStream(), FormatType.Docx);
        } catch (Exception e) {
            e.printStackTrace();
            return "{\"sections\":[{\"blocks\":[{\"inlines\":[{\"text\":" + e.getMessage() + "}]}]}]}";
        }
  }
```

## Paste with formatting

The following code converts the HTML, RTF content from client Clipboard to SFDT file and sends the converted SFDT to client for pasting formatted content in DocumentEditor.

```java
  @CrossOrigin(origins = "*", allowedHeaders = "*")
  @PostMapping("/api/wordeditor/SystemClipboard")
  public String systemClipboard(@RequestBody CustomParameter param) {
      if (param.content != null && param.content != "") {
          try {
              //Convert the pasted content into sfdt.
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

The following code computes HASH for the specified password and sends the generated HASH to client for protecting the Word document in DocumentEditor.

```java
  @CrossOrigin(origins = "*", allowedHeaders = "*")
  @PostMapping("/api/wordeditor/RestrictEditing")
  public String[] restrictEditing(@RequestBody CustomRestrictParameter param) throws Exception {
      if (param.passwordBase64 == "" && param.passwordBase64 == null)
          return null;
      //Compure hash value for the specified password.
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

>Note: Please refer the [Java Web API example from GitHub](https://github.com/SyncfusionExamples/EJ2-DocumentEditor-WebServices/tree/master/Java).