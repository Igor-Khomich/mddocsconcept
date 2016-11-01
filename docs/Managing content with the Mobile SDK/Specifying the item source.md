The item identifications parameters such as the item ID or the item path
may be not sufficient to identify the item precisely. The content you
retrieve based on these parameters may differ depending on the database
in which Sitecore stores items, the language and the numeric version of
the item.

To specify the item source, use the following item request configuration
parameters:

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
