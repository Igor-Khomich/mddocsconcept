When you request Sitecore items, all the requests are executed
asynchronously by the *ISitecoreSSCSession* interface instance. The SDK
contains the corresponding class, but it should not be instantiated
directly.

*ISitecoreSSCSession* provides two overloads for the ReadItemAsync()
method to process the requests based on one of the [item identification
parameters](373D2141-9C63-40C6-A904-877B96AA89F8) -
*IReadItemsByIdRequest* and *IReadItemsByPathRequest*. For example:

ScItemsResponse response = await session.ReadItemAsync(request);

If you cannot use the async keyword with your method, use the
Task.WaitAll() method instead:

var readHomeItemTask = session.ReadItemAsync(request);

Task.WaitAll(readHomeItemTask);

ScItemsResponse items = readHomeItemTask.Result;

To create, edit or remove items, use the following session methods:

-   CreateItemAsync – for creating items.

-   UpdateItemAsync – for editing items.

-   RunSitecoreSearchAsync – for searching items.

-   DeleteItemAsync – for removing items.
