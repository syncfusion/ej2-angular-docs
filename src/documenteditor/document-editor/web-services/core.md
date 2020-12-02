---
title: "DocumentEditor web services"
component: "DocumentEditor"
description: "Learn how to create web service in ASP.NET Core platform for Import, RestrictEditing, Paste with formatting and Spell check."
---

# Creating DocumentEditor web service in ASP.NET Core

DocumentEditor depends on server side interaction for below listed operations can be written in ASP.NET Core using [Syncfusion.EJ2.WordEditor.AspNet.Core](https://www.nuget.org/packages/Syncfusion.EJ2.WordEditor.AspNet.Core).

* Import Word Document
* Paste with formatting
* Restrict Editing
* Spell Check

This section explains how to create the service for DocumentEditor in ASP.NET Core.

## Importing Word Document

Word documents can be imported to DocumentEditor using the below code snippet.

```csharp
[AcceptVerbs("Post")]
[HttpPost]
[EnableCors("AllowAllOrigins")]
[Route("Import")]
public string Import(IFormCollection data)
{
    if (data.Files.Count == 0)
        return null;
    Stream stream = new MemoryStream();
    IFormFile file = data.Files[0];
    int index = file.FileName.LastIndexOf('.');
    string type = index > -1 && index < file.FileName.Length - 1 ?
        file.FileName.Substring(index) : ".docx";
    file.CopyTo(stream);
    stream.Position = 0;

    WordDocument document = WordDocument.Load(stream, GetFormatType(type.ToLower()));
    string json = Newtonsoft.Json.JsonConvert.SerializeObject(document);
    document.Dispose();
    return json;
}
```

## Paste with formatting

Paste with formatting action is defined in the below code snippet.

```csharp
[AcceptVerbs("Post")]
[HttpPost]
[EnableCors("AllowAllOrigins")]
[Route("SystemClipboard")]
public string SystemClipboard([FromBody]CustomParameter param)
{
    if (param.content != null && param.content != "")
    {
        try
        {
            WordDocument document = WordDocument.LoadString(param.content, GetFormatType(param.type.ToLower()));
            string json = Newtonsoft.Json.JsonConvert.SerializeObject(document);
            document.Dispose();
            return json;
        }
        catch (Exception)
        {
            return "";
        }
    }
    return "";
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
[AcceptVerbs("Post")]
[HttpPost]
[EnableCors("AllowAllOrigins")]
[Route("RestrictEditing")]
public string[] RestrictEditing([FromBody]CustomRestrictParameter param)
{
    if (param.passwordBase64 == "" && param.passwordBase64 == null)
        return null;
    return WordDocument.ComputeHash(param.passwordBase64, param.saltBase64, param.spinCount);
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
[AcceptVerbs("Post")]
[HttpPost]
[EnableCors("AllowAllOrigins")]
[Route("SpellCheck")]
public string SpellCheck([FromBody] SpellCheckJsonData spellChecker)
{
    try
    {
        SpellChecker spellCheck = new SpellChecker(spellDictionary);
        spellCheck.GetSuggestions(spellChecker.LanguageID, spellChecker.TexttoCheck, spellChecker.CheckSpelling, spellChecker.CheckSuggestion, spellChecker.AddWord);
        return Newtonsoft.Json.JsonConvert.SerializeObject(spellCheck);
    }
    catch
    {
        return "{\"SpellCollection\":[],\"HasSpellingError\":false,\"Suggestions\":null}";
    }
}

[AcceptVerbs("Post")]
[HttpPost]
[EnableCors("AllowAllOrigins")]
[Route("SpellCheckByPage")]
public string SpellCheckByPage([FromBody] SpellCheckJsonData spellChecker)
{
    try
    {
        SpellChecker spellCheck = new SpellChecker(spellDictionary);
        spellCheck.CheckSpelling(spellChecker.LanguageID, spellChecker.TexttoCheck);
        return Newtonsoft.Json.JsonConvert.SerializeObject(spellCheck);
    }
    catch
    {
        return "{\"SpellCollection\":[],\"HasSpellingError\":false,\"Suggestions\":null}";
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

>Note: Please refer the [ASP.NET Core Web API sample](https://github.com/SyncfusionExamples/EJ2-DocumentEditor-WebServices/tree/master/ASP.NET%20Core).