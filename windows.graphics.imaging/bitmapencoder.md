---
-api-id: T:Windows.Graphics.Imaging.BitmapEncoder
-api-type: winrt class
---

<!-- Class syntax.
public class BitmapEncoder : Windows.Graphics.Imaging.IBitmapEncoder, Windows.Graphics.Imaging.IBitmapEncoderWithSoftwareBitmap
-->

# Windows.Graphics.Imaging.BitmapEncoder

## -description
Contains methods to create, edit and save images.

## -remarks
### Image formats

[BitmapEncoder](bitmapencoder.md) can encode the following formats.

+ JPEG
+ PNG
+ GIF
+ TIFF
+ BMP
+ JPEG-XR
For a list of decoding formats, see the [BitmapDecoder](bitmapdecoder.md) topic.

[BitmapEncoder](bitmapencoder.md) behaves differently from [BitmapDecoder](bitmapdecoder.md) in that it doesn't provide random access to the frames in an image. Instead, you need to perform actions on the encoder in a specific order.

When you create a [BitmapEncoder](bitmapencoder.md), it provides access to data on the container and the first frame. When you are done setting data on the first frame and container, if you don't want to encode any additional frames, then call [FlushAsync](bitmapencoder_flushasync.md) to complete the encoding operation.

If you want to encode an additional frame, call [GoToNextFrameAsync](bitmapencoder_gotonextframeasync.md). This commits the data in the container and the first frame so you can't edit them anymore. At this point any actions you perform on the encoder will affect the second frame. After you are done with each frame, you can call [GoToNextFrameAsync](bitmapencoder_gotonextframeasync.md) to commit and append a new frame, or call [FlushAsync](bitmapencoder_flushasync.md) to finish.Bitmap encoders may expose various encoding options that affect the quality, size and other properties of the encoded output file. For more info, see [Imaging](http://msdn.microsoft.com/library/3fd2aa71-ef67-47b2-9332-3ffa5d3703ea).

## -examples
Here's a partial example of creating an encoder object. This example assumes you selected a file with [Windows.Storage.Pickers.FileSavePicker](../windows.storage.pickers/filesavepicker.md). For full instructions on selecting a file, creating an encoder, and encoding an image see [Imaging](http://msdn.microsoft.com/library/3fd2aa71-ef67-47b2-9332-3ffa5d3703ea)

```javascript
file.openAsync(Windows.Storage.FileAccessMode.readWrite).then(function (_stream) {
        stream = _stream;

        var encoderId;
        switch (fileType) {
            case ".jpg":
                encoderId = Windows.Graphics.Imaging.BitmapEncoder.jpegEncoderId;
                break;
        }
        return Windows.Graphics.Imaging.BitmapEncoder.createAsync(encoderId, stream);
        }).then(function (encoder) {

              // Your code here.
        }

```



## -see-also
[Imaging](http://msdn.microsoft.com/library/3fd2aa71-ef67-47b2-9332-3ffa5d3703ea), [Camera resolution sample (Windows 10)](http://go.microsoft.com/fwlink/p/?LinkId=624252), [Basic camera app sample (Windows 10)](http://go.microsoft.com/fwlink/p/?LinkId=619479), [Video stabilization sample (Windows 10)](http://go.microsoft.com/fwlink/p/?LinkId=620519), [Camera face detection sample (Windows 10)](http://go.microsoft.com/fwlink/p/?LinkId=619486), [Manual camera controls sample (Windows 10)](http://go.microsoft.com/fwlink/p/?LinkId=627611), [High dynamic range sample (Windows 10)](http://go.microsoft.com/fwlink/p/?LinkId=620517)