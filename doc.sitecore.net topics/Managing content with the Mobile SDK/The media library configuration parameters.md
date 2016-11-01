You can use the Mobile SDK 2.0 (SSC-only) to download files from the
media library of a Sitecore instance.

## The Media Library Root parameter

To request a media item, the API can use either the full item path or a
media path that is relative to the media library root folder. To specify
the root folder, use the MediaLibraryRoot parameter.

  Property              Details
  --------------------- ----------------------------------------------------------------
  Session builder API   MediaLibraryRoot(string)
  Sample value          “/sitecore/media library”
  Parameter position    Any position after the Instance URL and Credentials parameters

Usage guidelines:

-   This parameter is optional for all session types.

-   You cannot invoke this parameter several times in a session –
    multiple invocations cause *InvalidOperationException*.

-   The value must begin with a forward slash.

At the time of session initialization, you can change the root folder of
the media library that is specified on the server:

SitecoreSSCSessionBuilder.AnonymousSessionWithHost(“http://my-host.com”)

.MediaLibraryRoot("/sitecore/media library")

.BuildSession();

<span id="_The_Media_Prefix" class="anchor"><span
id="_The_Default_Media" class="anchor"><span id="_The_Media_Resizing"
class="anchor"></span></span></span>
