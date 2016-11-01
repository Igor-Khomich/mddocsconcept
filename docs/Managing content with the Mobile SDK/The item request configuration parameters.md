Mobile SDK 2.0 (SSC-only) includes functionality to create, retrieve,
delete, and update items in the Sitecore instance. The [request
builder](EE4A9135-7820-43A3-9136-1A68CCFB56B6) syntax is identical for
all the types of item requests. However, the scope of applicable methods
varies depending on the operation type. This topic outlines the usage
guidelines for the item request methods and parameters.

The Mobile SDK provides a set of methods to define the following
properties:

-   [Database](#the-database-database-method)

-   [Language](#_The_Language_(language))

-   [Version](#the-version-version-method)

-   [Fields](#the-addfieldstoread-fields-method)

-   [Paging](#the-itemsperpage-perpage-and-pagenumber-page-methods)

-   [Standard fields](#the-icludestanderdtemplatefields-method)

-   Sorting

-   

### The Database (database) method

To configure the database to get items from, use the Database() method.

  Property                           Details
  ---------------------------------- ------------------
  Mobile SDK 2.0 (SSC-only) method   Database(string)
  Item Service API parameter         database

<span id="_The_Language_(language)" class="anchor"></span>Usage
guidelines:

-   This is an optional parameter.

-   You cannot invoke this method several times in a request – multiple
    invocations cause *InvalidOperationException*.

-   The value must contain at least one symbol besides
    whitespace characters.

### The Language (language) method

To define the item language, use the Language() method.

  Property                           Details
  ---------------------------------- ------------------
  Mobile SDK 2.0 (SSC-only) method   Language(string)
  Item Service API parameter         language

Usage guidelines:

-   The language parameter is not applicable to item deletion requests.

-   This is an optional parameter.

-   You cannot invoke this method several times in a request – multiple
    invocations cause *InvalidOperationException*.

-   The value must contain at least one symbol besides
    whitespace characters.

### The Version (version) method

To define the item version, use the Version() method. To retrieve the
latest version of an item, do not invoke this method.

  Property                           Details
  ---------------------------------- ---------------
  Mobile SDK 2.0 (SSC-only) method   Version(int?)
  Item Web API parameter             version

Usage guidelines:

-   This is an optional parameter.

-   You cannot invoke this method several times in a request – multiple
    invocations cause *InvalidOperationException*.

-   You can only use null or integer numbers as the value.

-   Pass a positive number to get a specific version of an item.

### The AddFieldsToRead (fields) method

To explicitly set the item fields to be retrieved, use the
AddFieldsToRead() method.

  --------------------------------------------------------------------------
  Property                            Details
  ----------------------------------- --------------------------------------
  Mobile SDK 2.0 (SSC-only) methods   AddFieldsToRead(string)
                                      
                                      AddFieldsToRead(IList&lt;string&gt;)

  Item Service API parameter          fields
  --------------------------------------------------------------------------

<span id="_The_AddScope_(scope)" class="anchor"></span>Usage guidelines:

-   This is an optional parameter.

-   You can invoke this method several times in a request – multiple
    invocations accumulate values in invocation order.

-   The value must contain at least one symbol besides
    whitespace characters.

-   Field names cannot be null or empty.

### The ItemsPerPage (perPage) and PageNumber (page) methods

If the request returns a large dataset, for example, a news feed, a
photo stream, or search results, loading the whole content may take a
long time and cause memory warnings. To avoid this, the Sitecore Item
Service API service and the SSC SDK enable you to load data as a series
of chunks.

To split a server response into chunks, use the ItemsPerPage() and
PageNumber() methods.

  Property                           Details
  ---------------------------------- -------------------
  Mobile SDK 2.0 (SSC-only) method   ItemsPerPage(int)
  Item SErvice API parameter         pageSize

Usage guidelines:

-   This is an optional parameter.

-   You cannot invoke this method several times in a request – multiple
    invocations cause *InvalidOperationException*.

-   The value must be a positive number or you get the
    *ArgumentException* exception.

  Property                           Details
  ---------------------------------- ---------------------------------------
  Mobile SDK 2.0 (SSC-only) method   PageNumber(int)
  Item Service API parameter         page
  Value range                        0 to TotalItemsCount/ItemsPerPage + 1

Usage guidelines:

-   This is an optional parameter.

-   You cannot invoke this method several times in a request – multiple
    invocations cause *InvalidOperationException*.

-   The value must be a positive number or zero or you get the
    *ArgumentException* exception.

You must either specify both parameters or omit both of them, otherwise
the code does not compile.

var request = ItemSSCRequestBuilder.SitecoreSearchRequest(“home”)

.PageNumber(0)

.ItemsPerPage(2)

.Build();

var response = await this.session.RunSitecoreSearchAsync(request);

The paging options are only available for reading requests because other
operations on items do not require partial execution.

### The IcludeStanderdTemplateFields Method {#the-icludestanderdtemplatefields-method .ListParagraph}

To define the default fields set, use the
includeStandardTemplateFields() method.

If true, the standard template fields are part of the data that is
retrieved.

  Property                            Details
  ----------------------------------- ------------------------------------------------------------------------
  Mobile SDK 2.0 (SSC-only) methods   includeStandardTemplateFields(bool)
  ItemService API parameter           includeStandardTemplateFields
  Required/optional                   Optional, default value is false
  Multiple invocations                Multiple invocations are forbidden and cause InvalidOperationException
  Value validation                    Must contain bool value

### The Sorting Method {#the-sorting-method .ListParagraph}

To sort results for RunSitecoreSearchAsync method use the
AddDescendingFieldsToSort()\
and AddAscendingFieldsToSort() methods.

  ------------------------------------------------------------------------------------------------
  Property                            Details
  ----------------------------------- ------------------------------------------------------------
  Mobile SDK 2.0 (SSC-only) methods   AddDescendingFieldsToSort(string)
                                      
                                      AddDescendingFieldsToSort(IList&lt;string&gt;)
                                      
                                      AddAscendingFieldsToSort(string)
                                      
                                      AddAscendingFieldsToSort(IList&lt;string&gt;)

  ItemService API parameter           sorting

  Required/optional                   Optional

  Multiple invocations                Multiple invocations accumulate values in invocation order

  Value validation                    -   Must contain at least one symbol besides whitespaces
                                      
                                      -   Field names cannot be null or empty
                                      
                                      
  ------------------------------------------------------------------------------------------------
