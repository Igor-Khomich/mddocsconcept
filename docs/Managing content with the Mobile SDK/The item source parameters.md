Because Sitecore stores items in different databases and languages, you
may need to [construct a session](584A8568-AB80-4323-AA48-924720E3C18D)
that requests items in a particular language from a particular database.
To do that, use the DefaultDatabase and DefaultLanguage parameters:

var session =
SitecoreSSCSessionBuilder.AnonymousSessionWithHost(instanceUrl)

.DefaultDatabase("web")

.DefaultLanguage("en")

.BuildSession();

## The Default Database Parameter

  Property              Details
  --------------------- ----------------------------------------------------------------
  Session builder API   DefaultDatabase(string)
  Sample value          “master”, “web”, “core”
  Parameter position    Any position after the Instance URL and Credentials parameters

<span id="_Toc405900293" class="anchor"></span>Usage guidelines:

-   This parameter is optional for all session types.

-   You cannot invoke this parameter several times in a session –
    multiple invocations cause *InvalidOperationException*.

-   The value must contain at least one symbol besides
    whitespace characters.

## The Default Language Parameter

  Property              Details
  --------------------- ----------------------------------------------------------------
  Session builder API   DefaultLanguage(string)
  Sample value          “en”, “da”, “fr”, “ger”, “ja”, “cn”
  Parameter position    Any position after the Instance URL and Credentials parameters

Usage guidelines:

-   This parameter is optional for all session types.

-   You cannot invoke this parameter several times in a session –
    multiple invocations cause *InvalidOperationException*.

-   The value must contain at least one symbol besides
    whitespace characters.

Because the builder is order insensitive and both the DefaultDatabase
and the DefaultLanguage parameters are optional, you can specify either
both of them, or one of them, or none, for example:

var session =
SitecoreSSCSessionBuilder.AnonymousSessionWithHost(instanceUrl)

.DefaultDatabase("web")

.BuildSession();

Or:

var session =
SitecoreSSCSessionBuilder.AnonymousSessionWithHost(instanceUrl)

.DefaultLanguage("en")

.BuildSession();

Or:

var session =
SitecoreSSCSessionBuilder.AnonymousSessionWithHost(instanceUrl)

.BuildSession();

You can override the default source settings by resetting them in the
request object.
