To retrieve the media content using the Mobile SDK 2.0 (SSC-only), you
should construct and pass a request to a corresponding session building
method.

// constructing a request

string mediaPath = "/Images/green\_mineraly1";

var request =
ItemSSCRequestBuilder.DownloadResourceRequestWithMediaPath(mediaPath).Build();

// processing the request

using ( Stream response = await
this.session.DownloadMediaResourceAsync(request) )

{

// working with the media resource stream

}

Classes that process images differ between platforms, for example:

  Platform        Class name
  --------------- -------------
  iOS             UIImage
  Android         Bitmap
  Windows Phone   BitmapImage

Also, the requested media content may be not an image. For these
reasons, the user receives the media content stream after executing the
request.

Note

To avoid memory and resource leaks, you should wrap both the stream and
the image class in a using block.

## Setting Media Path

When you request a media resource, the first parameter that you should
pass to the request builder is the resource location.

The request builder accepts the following media paths:

-   The path relative to the Media Library root folder, which is the raw
    value of the **Image** field:

    "/Images/green\_mineraly1"

-   The absolute path of a media item in the Content Editor:

    "/Sitecore/Media Library/Images/green\_mineraly1"

-   The media URL fragment copied from a web browser:

    "\~/media/Images/green\_mineraly1.ashx"

    This fragment must begin with the [media
    hook](B459755A-8D73-417C-B1F1-05D44761EBC7) that has been specified
    at the time of session initialization.

You can use an absolute path or a media URL fragment for prototyping.
However, the safest approach is to use a relative media path.
