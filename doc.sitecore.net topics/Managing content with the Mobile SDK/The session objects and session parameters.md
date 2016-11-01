To send [Sitecore Services Client
requests](2FF12D3E-B47C-4C4E-BD18-7A164DBA533F), you need a session
object. Mobile SDK 2.0 (SSC-only) only provides a public interface for
the session. To create a session object, use the
SitecoreSSCSessionBuilder class API.

Session objects vary in permission types:

  ---------------------------------------------------
  Permission type         Session objects
  ----------------------- ---------------------------
  Security permissions    -   Anonymous session
                          
                          -   Authenticated session
                          
                          

  Operation permissions   -   ReadOnly session
                          
                          -   ReadWrite session
                          
                          
  ---------------------------------------------------

A session object stores the following session configuration parameters:

  -----------------------------------------------------------------------------------------------------------------------
  Parameter type                                                                       Session configuration parameters
  ------------------------------------------------------------------------------------ ----------------------------------
  [The connection endpoint parameters](1A70CCA7-B5EC-40F9-A9AD-2690E6AE6D62)           -   Instance URL
                                                                                       
                                                                                       -   Credentials
                                                                                       
                                                                                       

  [The item source parameters](07CEF13B-6641-46EE-9A82-36CEC18C56AC)                   -   Default database
                                                                                       
                                                                                       -   Default language
                                                                                       
                                                                                       

  [The Media Library configuration parameters](B459755A-8D73-417C-B1F1-05D44761EBC7)   -   Media Library root item
                                                                                       
                                                                                       
  -----------------------------------------------------------------------------------------------------------------------

You can pass the parameters one at a time in any order. For example:

var session =

SitecoreSSCSessionBuilder.AuthenticatedSessionWithHost(“http://my-host.com”)

.Credentials(loginAndPasswordProvider)

.DefaultDatabase("web")

.DefaultLanguage("en")

.MediaLibraryRoot("/sitecore/media library")

.BuildSession();

## Building sessions

Once you have set all the session configuration parameters, you can
invoke a builder method to create the session.

The Mobile SDK 2.0 (SSC-only) provides the following builder methods:

-   BuildReadonlySession()

    Use the BuildReadonlySession() method to create a read-only session
    to display the content stored in Sitecore without providing the
    ability to modify it. When you use this builder method, you must not
    invoke methods that change the content, or your code does
    not compile.

SitecoreSSCSessionBuilder.AnonymousSessionWithHost(“http://my-host.com”)

.BuildReadonlySession();

-   BuildSession()

    If users need to send data back to the Sitecore instance, use
    the BuildSession() method to create a standard session to allow both
    read and write access.

SitecoreSSCSessionBuilder.AnonymousSessionWithHost(“http://my-host.com”)

.BuildSession();
