The Mobile SDK 2.0 (SSC-only) includes the content editing API that lets
you send new raw values for items to the Sitecore instance and edit the
content in different databases and languages.

To update an item:

1.  [Identify the item](373D2141-9C63-40C6-A904-877B96AA89F8) that you
    want to update using the following request interfaces:

-   IUpdateItemByIdRequest – to identify the item by ID.

1.  If you want the update to affect a particular language, version, or
    database, specify the item source:

-   To update the item in a particular database, use the
    database parameter.

var request =
ItemSSCRequestBuilder.UpdateItemRequestWithId(“item-id-GUID”)

.Database(“master”)

.Build();

-   To pass a new value to a particular language version of the item,
    specify the language parameter.

var request =
ItemSSCRequestBuilder.UpdateItemRequestWithId(“item-id-GUID”)

.Language("en")

.AddFieldsRawValuesByNameToSet("Text", “Hello!”)

.Build();

var request =
ItemSSCRequestBuilder.UpdateItemRequestWithId(“item-id-GUID”)

.Language("de")

.AddFieldsRawValuesByNameToSet("Text", “Guten tag”)

.Build();

If you do not specify a language, the default language version is
updated with the new value.

-   To update a specific version of the item, use the version parameter.

var request =
ItemSSCRequestBuilder.UpdateItemRequestWithId(“item-id-GUID”)

.Language("en")

.Version(1)

.AddFieldsRawValuesByNameToSet("Text", “Hello!”)

.Build();

If you do not specify a version, the latest version of the item is
updated with the new value.

1.  Submit the [new field values](B53A1873-04C9-4E5F-8CAF-D11818D1A830),
    using the AddFieldsRawValuesByNameToSet() method.

var fields = new Dictionary&lt;string, string&gt;();

fields.Add(“Title”, “Device”);

fields.Add(“Text”, “Smartphone”);

var request =
ItemSSCRequestBuilder.UpdateItemRequestWithId(“item-id-GUID”)

**.AddFieldsRawValuesByNameToSet(fields)**

**.AddFieldsRawValuesByNameToSet("Manufacturer", “Unknown”)**

.Build();
