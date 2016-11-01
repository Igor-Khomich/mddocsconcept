Once you have set all the session configuration parameters, you can
invoke a builder method to create the session.

The SSC SDK provides the following builder methods:

-   BuildReadonlySession()

    Use the BuildReadonlySession() method to create a read-only session
    to display the content stored in the CMS without providing the
    ability to modify it. In this case, you must not invoke methods that
    change the content, or your code does not compile.

SitecoreSSCSessionBuilder.AnonymousSessionWithHost(“http://my-host.com”)

.BuildReadonlySession();

-   BuildSession()

    If users need to send data back to the Sitecore instance, use
    the BuildSession() method to create a standard session to allow both
    read and write access.

SitecoreSSCSessionBuilder.AnonymousSessionWithHost(“http://my-host.com”)

.BuildSession();
