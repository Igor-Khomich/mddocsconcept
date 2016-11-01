You can use the Mobile SDK 2.0 (SSC-only) to create, retrieve, delete,
update and search items in the Sitecore instance. To request a specific
item, you should identify it by one of the following parameters:

-   Item ID

-   Item Path

-   Search request

You submit the item identification parameters as string objects, so you
can submit any values. However, to be correctly processed by the
Sitecore Services Client REST service, they must conform to a set of
[validation rules](#validating-the-item-identification-parameters).

When these item identifications parameters are not sufficient to
identify the item precisely, you can [specify the item
source](#specifying-the-item-source).

The Mobile SDK 2.0 (SSC-only) does not let you request an item by more
than one parameter at a time, therefore, there are two separate request
objects for retrieving items:

-   IReadItemsByIdRequest

-   IReadItemsByPathRequest

All requests are immutable read-only interfaces. To generate these
requests, use the ItemSSCRequestBuilder class:

var request = ItemSSCRequestBuilder.ReadItemsRequestWithId(id).Build();

var request =
ItemSSCRequestBuilder.ReadItemsRequestWithPath(path).Build();

var request = ItemSSCRequestBuilder.SitecoreSearchRequest(text).Build();

## Validating the Item Identification Parameters

The Sitecore Services Client REST service cannot process certain values
of the item parameters, for example, it cannot read an item that you do
not have access to or locate an item by an incorrectly formatted
parameter. To prevent errors, the Mobile SDK 2.0 (SSC-only) validates
the submitted item parameters before passing them to the Sitecore
Services Client service. It performs the validation on the client
whenever possible. If the validation fails, the SDK throws an exception.

The following validation rules are applied to item identification
parameters:

-   Item ID – the string should contain a GUID, which is a 128-bit
    number separated by hyphens:

const string itemId = "3D6658D8-QQQQ-QQQQ-B3E2-D050FABCF4E1";

The hyphens are required. If you pass a string that is null, empty, or
consists only of whitespace characters, the request builder throws an
exception. In case of other errors, the request is sent to the server,
which returns an appropriate response or an error.

-   Item Path – the absolute path to the item, beginning with a forward
    slash:

const string itemPath = "/sitecore/content/Home";

The leading forward slash is required. If you omit the slash, the
request builder throws an *ArgumentException*. If you pass a string that
is null, empty, or consists only of whitespace characters, the request
builder throws an exception.

## Specifying the item source

The item identifications parameters such as the item ID or the item path
may be not sufficient to identify the item precisely. The content you
retrieve based on these parameters may differ depending on the database
in which Sitecore stores the item as well as its language and numeric
version.

To specify the item source, use the following [item request
configuration parameters](A6FB5C63-03C7-4943-826D-36CC708A7627):

-   database – to specify a database.

-   language – to specify a language version.

-   version – to specify a numeric version.

You can configure the item source in the following ways:

-   Per request on the client – the item source parameters are defined
    in the item request. The values from the request are a top priority.

-   Per session on the client – if the request doesn’t contain the item
    source parameters, the SDK uses the values from the
    *ISitecoreSSCSession.DefaultSource* property of the current session.

-   On the server – if neither the request nor the session contains the
    item source parameters, the SDK does not pass any values to
    the server. In this case, the server uses its own default values
    configured by the administrator to define the item source.

The item source is an important parameter that affects both item
retrieval and caching. Therefore, you should specify the item source
explicitly to always control where the content comes from.

However, to ensure that you retrieve the latest version of the item, you
can omit the version parameter.
