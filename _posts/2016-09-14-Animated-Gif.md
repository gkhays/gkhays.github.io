# Animated GIF

This article describes the process for creating an animated GIF file. It includes procedures for Windows and Mac OS X.

## Windows

The first step is to obtain a screen capture of the event that is to be depicted in the animated GIF. I used the free Expression Encoder 4.

![Expression Screen Capture](/images/Expression-ScreenCap.png)

Once the screen has been captured, it must be encoded to a video format. In the case of the free version of Expression Encoder, only the Window Media Video (WMV) codec is supported. In any case, the first step is to send the capture to the separate Expression Encoder utility.

![Export to Encoder](/images/Expression-ScreenCapExport-To-Encoder.png)

The "Send to Encoder" button will open Expression Encoder with the capture project. At this point we may now encode to the WMV format.

![Encode WMV](/images/EncodeWMV.png)

There are several tools for converting video files to an animated GIF but the one I use most often is [gifify](https://github.com/jclem/gifify).

However, my installation of Cygwin did not have ffmpeg or imagemagick nor did I have the GnuWin versions. So I decided to run gifify on an Ubuntu workstation.

I had some problems getting the correct dependencies (ffmpeg and imagemagick convert) installed on Ubuntu so I used [gifify-docker](https://github.com/maxogden/gifify-docker) instead.

![gifify-docker](/images/gifify-docker.png)

```bash
$ docker run -it --rm -v $(pwd):/data maxogden/gifify source.mp4 -o output.gif
```

## Mac

![Handbrake](/images/Handbrake2MP4.png)