When you have configured a request with all the necessary
[parameters](A6FB5C63-03C7-4943-826D-36CC708A7627), you can build the
request. Invoke the Build() method to get the request object.

var request =

ItemSSCRequestBuilder.ReadItemsRequestWithPath("/sitecore/content/home")

.Database("master")

.Language("fr")

.AddFieldsToRead("Name")

.AddFieldsToRead("Photo")

.IcludeStanderdTemplateFields(true)

.Build();

When you build a request, you must observe the following rules:

-   Define the item identification parameter first. Define optional
    parameters in any order.

    Correct requests:

ItemSSCRequestBuilder.ReadItemsRequestWithPath("/sitecore/content/home")

.Database("master")

.Language("fr")

.Build();

Or:

ItemSSCRequestBuilder.ReadItemsRequestWithPath("/sitecore/content/home")

.Language("fr")

.Database("master")

.Build();

An incorrect request:

var request = ItemSSCRequestBuilder.Database("master")

.ReadItemsRequestWithPath("/sitecore/content/home")

.Build();

// This will not compile

-   The Add… methods accumulate values, so consider the
    invocation order.

    For example, the following request retrieves the *Home* item and its
    two fields: the **Name** field and the **Photo** field.

ItemSSCRequestBuilder.ReadItemsRequestWithPath("/sitecore/content/home")

.AddFieldsToRead("Name")

.AddFieldsToRead("Photo")

.Build();

-   Invoke methods that don’t accumulate values only once.

    A correct request:

ItemSSCRequestBuilder.ReadItemsRequestWithPath("/sitecore/content/home")

.Database("web")

.Language("en")

.Build();

An incorrect request that throws *InvalidOperationException*:

ItemSSCRequestBuilder.ReadItemsRequestWithPath("/sitecore/content/home")

.Database("master")

.Language("fr")

.Database("web")

.Language("en")

.Build();
