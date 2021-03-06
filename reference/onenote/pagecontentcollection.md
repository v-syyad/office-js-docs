# PageContentCollection Object (JavaScript API for OneNote)

_Applies to: OneNote Online_
_Note: This API is in preview_

Represents the contents of a page, as a collection of PageContent objects.

## Properties

| Property	   | Type	|Description
|:---------------|:--------|:----------|
|count|int|Returns the number of page contents in the collection. Read-only.|
|items|[PageContent[]](pagecontent.md)|A collection of pageContent objects. Read-only.|

_See property access [examples.](#property-access-examples)_

## Relationships
None


## Methods

| Method		   | Return Type	|Description|
|:---------------|:--------|:----------|
|[getItem(index: number or string)](#getitemindex-number-or-string)|[PageContent](pagecontent.md)|Gets a PageContent object by ID or by its index in the collection. Read-only.|
|[getItemAt(index: number)](#getitematindex-number)|[PageContent](pagecontent.md)|Gets a page content on its position in the collection.|
|[load(param: object)](#loadparam-object)|void|Fills the proxy object created in JavaScript layer with property and object values specified in the parameter.|

## Method Details


### getItem(index: number or string)
Gets a PageContent object by ID or by its index in the collection. Read-only.

#### Syntax
```js
pageContentCollectionObject.getItem(index);
```

#### Parameters
| Parameter	   | Type	|Description|
|:---------------|:--------|:----------|
|index|number or string|The ID of the PageContent object, or the index location of the PageContent object in the collection.|

#### Returns
[PageContent](pagecontent.md)

### getItemAt(index: number)
Gets a page content on its position in the collection.

#### Syntax
```js
pageContentCollectionObject.getItemAt(index);
```

#### Parameters
| Parameter	   | Type	|Description|
|:---------------|:--------|:----------|
|index|number|Index value of the object to be retrieved. Zero-indexed.|

#### Returns
[PageContent](pagecontent.md)

### load(param: object)
Fills the proxy object created in JavaScript layer with property and object values specified in the parameter.

#### Syntax
```js
object.load(param);
```

#### Parameters
| Parameter	   | Type	|Description|
|:---------------|:--------|:----------|
|param|object|Optional. Accepts parameter and relationship names as delimited string or an array. Or, provide [loadOption](loadoption.md) object.|

#### Returns
void
### Property access examples

**items**
```js
OneNote.run(function (context) {

    // Get the collection of pageContent items from the page.
    var pageContents = context.application.getActivePage().getContents();

    // Queue a command to load the type of each pageContent.
    pageContents.load("type");

    // Run the queued commands, and return a promise to indicate task completion.
    return context.sync()
        .then(function () {

            $.each(pageContents.items, function(index, pageContent) {
                console.log("PageContent type: " + pageContent.type);
            });
        });
    })                
    .catch(function(error) {
        console.log("Error: " + error);
        if (error instanceof OfficeExtension.Error) {
            console.log("Debug info: " + JSON.stringify(error.debugInfo));
        }
    });
```