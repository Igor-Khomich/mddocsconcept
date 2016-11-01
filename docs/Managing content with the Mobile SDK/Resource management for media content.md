## 

To store media content, you need additional traffic and memory
resources. Therefore, you should release unmanaged resources as soon as
possible, which means to properly dispose all the instances of the
IDisposable interface and of the following classes of native platforms:

-   Stream and its subclasses

-   NSData (iOS)

-   UIImage (iOS)

-   Bitmap (Android)

For example:

string path = “/images/SitecoreLogo.png”;

var request =
ItemSSCRequestBuilder.DownloadResourceRequestWithMediaPath(path).Build();

byte\[\] data = null;

// getting the network stream from a session

using (Stream response = await
session.DownloadMediaResourceAsync(request))

using (MemoryStream responseInMemory = new MemoryStream())

{

// copying contents to memory of filesystem

await response.CopyToAsync(responseInMemory);

// Now we can convert the byte array to NSData

data = responseInMemory.ToArray();

}

using ( NSData imageData = NSData.FromArray(data) )

using ( UIImage image = new UIImage(imageData) )

{

// no need managing the ImageView field

// since this.ImageView.Image creates a

// new C\# object on each call

this.ImageView.Image = image;

}
