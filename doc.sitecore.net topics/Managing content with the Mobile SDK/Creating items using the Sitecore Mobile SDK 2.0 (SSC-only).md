The Mobile SDK 2.0 (SSC-only) lets you create new Sitecore items via the
API.

To create a new item, you must pass a request that specifies item
parameters to the ISitecoreSSCSession.CreateItemAsync() method.

A sample item creation request:

var request =
ItemSSCRequestBuilder.CreateItemRequestWithParentPath("item-id-GUID")

.ItemTemplateId("item-id-GUID")

.ItemName(“Name of new item”)

.Build();

var createResponse = await session.CreateItemAsync(request);

When you construct a request to create a Sitecore item, you must:

-   [Set the item location](#setting-the-item-location).

-   [Set the item name](#setting-the-item-name).

-   [Set the item template](#setting-the-item-template).

-   (Optionally) [Set the item content](#setting-the-item-content).

You must specify the following parameters to create an item:

-   Item name

-   Item template ID

-   Parent item ID

Optionally, you can also specify the following item parameters:

-   Database

-   Language

-   Item fields

## Setting the item location

To create a new item in Sitecore, you must specify its location in the
content tree.

To set the item location, define the parent item by path:

var request =

ItemSSCRequestBuilder.CreateItemRequestWithParentParentPath("/path/to/parent")

.ItemTemplatePath(“GUID”)

.ItemName(“Name of new item”)

.Build();

In addition to the parent item, you can specify the low-level storage
parameters, such as, the item language and the database to store the
item in.

## Setting the item name

In order for the content of items to be accessible, each Sitecore item
must have a name.

To specify the name of the item, use the ItemName() method.

  Property                           Details
  ---------------------------------- -----------------------------
  Mobile SDK 2.0 (SSC-only) method   ItemName(string)
  Item Service API parameter         ItemName (The request body)

Usage guidelines:

-   This is a required parameter.

-   You cannot invoke this method several times in a request – multiple
    invocations cause *InvalidOperationException*.

-   The value must contain at least one symbol besides
    whitespace characters. You cannot use the following symbols in the
    item name:

<!-- -->

-   A period “.”

-   A dash “-“

-   A slash “/”

    To use the item name in both queries and XPATH expressions, you must
    conform to the value validation rules. Using forbidden symbols in
    the item name causes an exception, for example:

ItemSSCRequestBuilder.CreateItemRequestWithParentPath (parentPath)

.ItemName(“/item/sub-path”) // throws ArgumentException

The item name must be unique within a given folder. If you specify an
existing name, the Item Web API increments the item name automatically.

## Setting the item template

The item template defines the list of available fields of the item.

To set the template that you want new items to be based on, specify the
template ID.

### Specifying the template ID

To identify the item template by its ID, use the ItemTemplateId()
method.

  Property                     Details
  ---------------------------- -------------------------------
  SSC SDK method               ItemTemplateId(string)
  Item Service API parameter   TemplateID (The request body)

Usage guidelines:

-   This is a required parameter.

-   You cannot invoke this method several times in a request – multiple
    invocations cause *InvalidOperationException*.

-   The value must contain at least one symbol enclosed in braces.

A sample request:

var request =
ItemSSCRequestBuilder.CreateItemRequestWithParentPath(parentItemPath)

**.ItemTemplateId(“{GUID-ITEM-ID}”)**

.ItemName(“Name of new item”)

.Build();

## Setting the item content

To compile a list of field names and raw values for the item that you
create, use the AddFieldsRawValuesByNameToSet() method in the item
creation request.

  -----------------------------------------------------------------------------------------------
  Property                           Usage guidelines
  ---------------------------------- ------------------------------------------------------------
  Mobile SDK 2.0 (SSC-only) method   AddFieldsRawValuesByNameToSet(string key, string rawValue)
                                     
                                     AddFieldsRawValuesByNameToSet(IDictionary)

  Item Web API parameter             The request body
  -----------------------------------------------------------------------------------------------

Usage guidelines:

-   This is an optional parameter.

-   You can invoke this method several times in a request – multiple
    invocations accumulate values.

-   You cannot submit duplicate values.

-   Both the key and the value must contain at least one symbol besides
    whitespace characters.

To submit key-value pairs for the item fields, use one of the following
approaches:

-   Submit values one at a time:

var request =
ItemSSCRequestBuilder.CreateItemRequestWithParentPath(parentItemPath)

.ItemTemplateId(“GUID”)

.ItemName(“new item”)

**.AddFieldsRawValuesByNameToSet("Title", “Device”)**

**.AddFieldsRawValuesByNameToSet("Text", “Smartphone”)**

.Build();

-   Append a dictionary that contains the values:

// setup fields beforehand

**var fields = new Dictionary&lt;string, string&gt;();**

fields.Add(“Title”, “Device”);

fields.Add(“Text”, “Smartphone”);

//

var request =
ItemSSCRequestBuilder.CreateItemRequestWithParentPath(parentItemPath)

.ItemTemplateId(“GUID”)

.ItemName(“new item”)

**.AddFieldsRawValuesByNameToSet(fields)**

.Build();
