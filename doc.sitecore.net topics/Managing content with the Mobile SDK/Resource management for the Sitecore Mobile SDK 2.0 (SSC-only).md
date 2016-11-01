Because of memory and CPU limitations, mobile applications must use
resources efficiently. This topic describes the resource management
techniques that you can apply to optimize your resource allocation when
using the Mobile SDK 2.0 (SSC-only):

-   Resource management for Mobile SDK 2.0 (SSC-only) classes

-   [Resource management for media content](#_Resource_management_for_1)

## Resource management for Mobile SDK 2.0 (SSC-only) classes

Most classes and interfaces in the SDK are pure, managed objects.
However, the session holds references to native resources, for example,
a reference to the HttpClient instance, which uses a native socket. The
credentials provider can access a native, platform-specific keychain.

To properly release unmanaged resources, the session implements the
IDisposable interface, which requires that:

-   If you use the session as a local variable, you must declare and
    instantiate it in a using statement, which calls the Dispose method
    in the correct way and causes the session object to go out of scope
    as soon as the method is called:

using (var session =

SitecoreSSCSessionBuilder.AnonymousSessionWithHost(instanceUrl)

.DefaultDatabase("web")

.DefaultLanguage("en")

.MediaLibraryRoot("/sitecore/media library")

.MediaPrefix("\~/media/")

.DefaultMediaResourceExtension("ashx")

.BuildReadonlySession())

{

// Send some requests

}

-   If you store the session as an instance variable of your class, you
    must implement the IDisposable interface and dispose the session
    object explicitly:

void ReleaseResources()

{

if (null != this.session)

{

this.session.Dispose();

this.session = null;

}

}

public virtual void Dispose()

{

this.ReleaseResources();

GC.SuppressFinalize(this);

}

\~MyClassThatUsesSSCSession()

{

}

To ensure that your application disposes HttpClient and credentials
properly, wrap both the session and credentials in a using block.
Otherwise, the application may crash with a memory warning or with the
*Too many open files* exception.

The session owns the credentials provided on the initialization and
attempts to make a copy of them. If your implementation of the password
provider does not support copying, do not wrap it in a using block.

<span id="_Resource_management_for_1" class="anchor"></span>
