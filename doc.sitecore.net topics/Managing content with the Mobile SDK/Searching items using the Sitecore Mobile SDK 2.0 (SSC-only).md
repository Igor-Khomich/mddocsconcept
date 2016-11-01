You can use the Mobile SDK 2.0 (SSC-only) to search Sitecore items as
well.

To search an items, pass a request that specifies search parameters to
the ISitecoreSSCSession.RunSearchAsync() method.

var request = ItemSSCRequestBuilder.SitecoreSearchRequest(“home”)\
    .Build();

You can use Database() or Language() options to specify your items
source as usual.

### Stored Search

Also you can use Sitecore stored search request. You use this method to
run a search that is stored in a Sitecore item (“search definition
item”.)

The search definition item contains default values for things like root
item for the search, template type, and so forth. You pass the search
item Id to build the request.

var request = ItemSSCRequestBuilder.StoredSearchRequest(“search
definition item id”)\
            .Term(“home”)\
            .Build();

### Stored Query

To run the stored query request, call the
ISitecoreSSCSession.RunStoredQuerryAsync() method.

And pass the StoredQuerryRequest request to run a query that is stored
in a Sitecore item (a “query definition item”.)

var request = ItemSSCRequestBuilder.StoredQuerryRequest(“query
definition item id”)\
         .Build();

<span id="_Setting_the_item" class="anchor"><span
id="_Setting_the_Item_1" class="anchor"><span id="_Setting_the_Item_2"
class="anchor"><span id="_Setting_the_Item_3"
class="anchor"></span></span></span></span>
