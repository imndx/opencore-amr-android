opencore-amr-android
====================

An opencore amr codec JNI wrapper with explanation,
And one solution for packaging amr audio files.

### 中文文档请移步[README_CN](README_CN.md)
## QQ tribe for help: 453503476

## Background
- [opencore][1] is the multimedia framework of android, which is a originallly contributed by PacketVideo.
- [AMR][2] is abbreviation for Adaptive Multi-Rate audio codec, which is an audio compression format optimized for speech coding.
- [opencore-AMR][3] is extracted from opencore as an codec for amr<->pcm encode/decode

## What Is This
- Opencore-amr-dndroid is a wrapper for handy usage. You can usage wrapped api in Android Application without any troubles of writing c++ wrapper or ndk mk file.
- Demo project offer a solution for packaging amr audio files, in elegant code structure.

## Setup
- Android Studio

  1. Add jcenter as your repository in project's build.gradle:
  ```gradle
  allprojects {
        repositories {
            jcenter()//this is the default setting
        }
      }
  ```
  2. Add dependency in your module's build.gradle:
  ```gradle
  dependencies {
        compile fileTree(dir: 'libs', include: ['*.jar'])
        compile 'com.hikvh:opencore-amr-android:1.0.0'//this is the lib
  }
  ```

  OR: Copy the content if [library](library/) to your module, as follows:

  ![Integration](screenshot/android_studio_integration.png)

- ADT(Eclipse)
  Copy the content if [library](library/) to your project:
  > Copy content of libs and src to the corresponding folder

## Quick Start Up
- Call api like this:

``` java
    AmrEncoder.init(0);
    int mode = AmrEncoder.Mode.MR122.ordinal();
    short[] in;//short array read from AudioRecorder, recommend length 160
    byte[] out = new byte[in.length];
    int byteEncoded = AmrEncoder.encode(mode, in, out);
    AmrEncoder.exit();
```
there you go.

## Packaging amr audio to file system
> record->encode->package amr file->upload(not implemented)

Audio steam is packaged to file in slices, the slice last a few seconds(customizable). This policy is suitable for this scenario: client is under unstable mobile network, client records amr file, sends slice by slice, server re-assembles the slices.

If you are interested in this solution, please refer to [demo](demo/)


## FAQ
Please edit the FAQ files to help others, thanks! (赠人玫瑰，手留余香)

[FAQ_CN](FAQ_CN.md)

[FAQ](FAQ.md)

  [1]: https://github.com/android/platform_external_opencore
  [2]: http://en.wikipedia.org/wiki/Adaptive_Multi-Rate_audio_codec
  [3]: http://opencore-amr.sourceforge.net/
