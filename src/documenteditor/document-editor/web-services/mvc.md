---
title: "DocumentEditor web services"
component: "DocumentEditor"
description: "Learn how to create web service in ASP.NET MVC platform for Import, RestrictEditing, Paste with formatting and Spell check."
---

# Creating DocumentEditor web service in ASP.NET MVC

DocumentEditor depends on server side interaction for below listed operations can be written in ASP.NET MVC using [Syncfusion.EJ2.WordEditor.AspNet.Mvc5](https://www.nuget.org/packages/Syncfusion.EJ2.WordEditor.AspNet.Mvc5) or [Syncfusion.EJ2.WordEditor.AspNet.Mvc4](https://www.nuget.org/packages/Syncfusion.EJ2.WordEditor.AspNet.Mvc4).

* Import Word Document
* Paste with formatting
* Restrict Editing
* Spell Check

This section explains how to create the service for DocumentEditor in ASP.NET MVC.

## Importing Word Document

Word documents can be imported to DocumentEditor using the below code snippet.

```csharp
[HttpPost]
[EnableCors("*", "*", "*")]
[Route("Import")]
public HttpResponseMessage Import()
{
    if (HttpContext.Current.Request.Files.Count == 0)
        return null;

    HttpPostedFile file = HttpContext.Current.Request.Files[0];
    int index = file.FileName.LastIndexOf('.');
    string type = index > -1 && index < file.FileName.Length - 1 ?
        file.FileName.Substring(index) : ".docx";
    Stream stream = file.InputStream;
    stream.Position = 0;

    EJ2WordDocument document = EJ2WordDocument.Load(stream, GetFormatType(type.ToLower()));
    string json = Newtonsoft.Json.JsonConvert.SerializeObject(document);
    document.Dispose();
    return new HttpResponseMessage() { Content = new StringContent(json) };
}
```

## Paste with formatting

Paste with formatting action is defined in the below code snippet.

```csharp
[HttpPost]
[EnableCors("*", "*", "*")]
[Route("SystemClipboard")]
public HttpResponseMessage SystemClipboard([FromBody]CustomParameter param)
{
    if (param.content != null && param.content != "")
    {
        try
        {
            Syncfusion.EJ2.DocumentEditor.WordDocument document = Syncfusion.EJ2.DocumentEditor.WordDocument.LoadString(param.content, GetFormatType(param.type.ToLower()));
            string json = Newtonsoft.Json.JsonConvert.SerializeObject(document);
            document.Dispose();
            return new HttpResponseMessage() { Content = new StringContent(json) };
        }
        catch (Exception)
        {
            return new HttpResponseMessage() { Content = new StringContent("") };
        }

    }
    return new HttpResponseMessage() { Content = new StringContent("") };
}

public class CustomParameter
{
    public string content { get; set; }
    public string type { get; set; }
}
```

## Restrict editing

Restrict editing action is defined in the below code snippet.

```csharp
[HttpPost]
[EnableCors("*", "*", "*")]
[Route("RestrictEditing")]
public string[] RestrictEditing([FromBody]CustomRestrictParameter param)
{
    if (param.passwordBase64 == "" && param.passwordBase64 == null)
        return null;
    return Syncfusion.EJ2.DocumentEditor.WordDocument.ComputeHash(param.passwordBase64, param.saltBase64, param.spinCount);
}

public class CustomRestrictParameter
{
    public string passwordBase64 { get; set; }
    public string saltBase64 { get; set; }
    public int spinCount { get; set; }
}
```

## Spell Check

Spell check action is defined in the below code snippet.

```csharp
[HttpPost]
[EnableCors("*", "*", "*")]
[Route("SpellCheck")]
public HttpResponseMessage SpellCheck([FromBody] SpellCheckJsonData spellChecker)
{
    try
    {
        SpellChecker spellCheck = new SpellChecker(spellDictionary);
        spellCheck.GetSuggestions(spellChecker.LanguageID, spellChecker.TexttoCheck, spellChecker.CheckSpelling, spellChecker.CheckSuggestion, spellChecker.AddWord);
        string json = Newtonsoft.Json.JsonConvert.SerializeObject(spellCheck);
        return new HttpResponseMessage() { Content = new StringContent(json) };
    }
    catch
    {
        return new HttpResponseMessage() { Content = new StringContent("{\"SpellCollection\":[],\"HasSpellingError\":false,\"Suggestions\":null}") };
    }
}

[HttpPost]
[EnableCors("*", "*", "*")]
[Route("SpellCheckByPage")]
public HttpResponseMessage SpellCheckByPage([FromBody] SpellCheckJsonData spellChecker)
{
    try
    {
        SpellChecker spellCheck = new SpellChecker(spellDictionary);
        spellCheck.CheckSpelling(spellChecker.LanguageID, spellChecker.TexttoCheck);
        string json = Newtonsoft.Json.JsonConvert.SerializeObject(spellCheck);
        return new HttpResponseMessage() { Content = new StringContent(json) };
    }
    catch
    {
        return new HttpResponseMessage() { Content = new StringContent("{\"SpellCollection\":[],\"HasSpellingError\":false,\"Suggestions\":null}") };
    }
}

public class SpellCheckJsonData
{
    public int LanguageID { get; set; }
    public string TexttoCheck { get; set; }
    public bool CheckSpelling { get; set; }
    public bool CheckSuggestion { get; set; }
    public bool AddWord { get; set; }

}
```

>Note: Please refer the [ASP.NET MVC Web API sample](https://github.com/SyncfusionExamples/EJ2-DocumentEditor-WebServices/tree/master/ASP.NET%20MVC).