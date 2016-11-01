The Mobile SDK 2.0 (SSC-only) lets you delete items in the Sitecore
content tree from a .NET application via the API.

To delete an item use the following request interface:

-   IDeleteItemsByIdRequest – identify the item by ID.

1.  If you want to remove the item from a particular database, use the
    database parameter.

    The following request removes all the versions of the item in all
    the languages from the Master database:

var request = ItemSSCRequestBuilder.DeleteItemRequestWithId(itemId)

**.Database(“master”)**

.Build();

1.  Pass the request to the session:

var request = ItemSSCRequestBuilder.DeleteItemRequestWithId(itemId)

.Database(“master”)

.Build();

ScItemsResponse response = await session.DeleteItemAsync(request);
