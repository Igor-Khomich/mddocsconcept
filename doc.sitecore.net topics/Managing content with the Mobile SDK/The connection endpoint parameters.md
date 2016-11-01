When you start [configuring a
session](584A8568-AB80-4323-AA48-924720E3C18D), you should use the
connection endpoint parameters to define a host, authentication
credentials, and target site.

The Mobile SDK 2.0 (SSC-only) provides the following connection endpoint
parameters:

-   [Instance URL](#the-instance-url-parameter)

-   [Credentials](#the-credentials-parameter)

## The Instance URL parameter

The Instance URL parameter defines a session host – so it is the first
parameter that you use to invoke a session initializer.

  ------------------------------------------------------------
  Property              Details
  --------------------- --------------------------------------
  Session builder API   AnonymousSessionWithHost(string)
                        
                        AuthenticatedSessionWithHost(string)

  Sample value          http://my-site.com:80

  Parameter position    First in a sequence
  ------------------------------------------------------------

Usage guidelines:

-   This parameter is required for all session types.

-   You cannot invoke this parameter several times in a session –
    multiple invocations do not compile.

-   The value must contain at least one symbol besides
    whitespace characters.

-   If you do not specify the URL scheme in the Instance URL parameter,
    the default value is http. For example, my-site.com is resolved as
    <http://my-site.com>.

## The Credentials parameter

To restrict the access to your content, you should set up user
permissions in the Security Editor and pass the user name and password
to an authenticated session using the Credentials parameter:

var session =

SitecoreSSCSessionBuilder.AuthenticatedSessionWithHost(instanceUrl)

.Credentials(loginAndPasswordProvider)

.BuildSession();

To build an anonymous session, skip the Credentials parameter:

var session =

SitecoreSSCSessionBuilder.AnonymousSessionWithHost(instanceUrl)

.BuildSession();

  Property              Details
  --------------------- ----------------------------------------------
  Session builder API   Credentials(IScCredentials)
  Sample value          n/a
  Parameter position    Immediately after the Instance URL parameter

Usage guidelines:

-   This parameter is required for an authenticated session.

-   You cannot invoke this parameter several times in a session –
    multiple invocations do not compile.

-   The value must contain at least one symbol besides
    whitespace characters.

Mobile SDK 2.0 (SSC-only) accepts the credentials via the IScCredentials
interface. You can either use the default password provider or implement
a custom credentials provider.

The SDK provides default cross-platform implementation that pass user
credentials to web requests. The implementation use the string class to
store credentials, so this implementation is not secure, if you would
like to secure credentials you should implement a class derived from the
IScCredentials interface.

##
