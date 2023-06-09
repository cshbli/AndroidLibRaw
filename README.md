# Try it

You may directly download the pre-compiled apk `app-debug.apk` to test the current build on your phone.

# Change Logs

### Upgrade Sdk version from 31 to 34

```
Dependency 'androidx.core:core:1.12.0-alpha05' requires 'compileSdkVersion' to be set to 34 or higher.
Compilation target for module ':app' is 'android-31'

Dependency 'androidx.core:core-ktx:1.12.0-alpha05' requires 'compileSdkVersion' to be set to 34 or higher.
Compilation target for module ':app' is 'android-31'

Dependency 'androidx.annotation:annotation-experimental:1.3.0' requires 'compileSdkVersion' to be set to 33 or higher.
Compilation target for module ':app' is 'android-31'
```

Change `compileSdk` from 31 to 34
change `targetSdk` from 31 to 34

### Upgrade ext.kotlin_version from 1.6.10 to 1.8.20

```
Duplicate class kotlin.collections.jdk8.CollectionsJDK8Kt found in modules jetified-kotlin-stdlib-1.8.21 (org.jetbrains.kotlin:kotlin-stdlib:1.8.21) and jetified-kotlin-stdlib-jdk8-1.5.30 (org.jetbrains.kotlin:kotlin-stdlib-jdk8:1.5.30)
Duplicate class kotlin.internal.jdk7.JDK7PlatformImplementations found in modules jetified-kotlin-stdlib-1.8.21 (org.jetbrains.kotlin:kotlin-stdlib:1.8.21) and jetified-kotlin-stdlib-jdk7-1.6.10 (org.jetbrains.kotlin:kotlin-stdlib-jdk7:1.6.10)

Go to the documentation to learn how to Fix dependency resolution errors.
```

# Android LibRaw
Another Android LibRaw implementation.  LibRaw is used to render camera raw image files (e.g Nikon NEF, Canon CR2, Sony ARW).   The project contains a sample app that shows a simple implementation.


## Using the artifact
On the surface, this is as easy as:

`implementation 'com.homesoft.android:libraw:2.0.4'`

Might just be easier to download it from: 
https://github.com/dburckh/AndroidLibRaw/packages/1172747

## Cloning the Project
Because the project has submodule links, it requires an extra parameter.

`git clone --recurse-submodules https://github.com/cshbli/AndroidLibRaw.git`

A note on submodules:

If you want to new version of the LibRaw or LibRawCMake, you can update the submodules.  Use caution updating the actual LibRaw/LibRawCMake code, updating submodule code can be tricky.

## Building the libraw.aar
No pre-builts just yet, but you can build the aar from the command line:

`gradlew libraw::assemble`

It usually ends up under ./libraw/build/outputs/aar

## Benefits
- Decodes the actual raw data.  BitmapFactory shows the embedded JPEG, if available
- Works with modern Android File security constraints (uses FileDescriptors or File paths).
- Works with Kotlin or Java.
- Not a custom version of LibRaw!  Should work with future releases with little or no modification.
- Uses CMake build system.

## Limitations
- Requires API 24+ (Nougat).
- Uses NDK 22, (21 is the current default).
- Uses Git Submodules.
- TODO: Unit tests

## Sources
Most of the code I did for this was either glue or tweaking of somebody else work.
- [LibRaw](https://github.com/LibRaw/LibRaw) The brains of the operation
- [LibRaw-cmake](https://github.com/LibRaw/LibRaw-cmake) Made building LibRaw in Studio/gradle, much easier.
- [LibRaw-Android](https://github.com/TSGames/Libraw-Android) Ground breaking "glue" code I borrowed heavily from.

### Change Log
2.0.4
- Add Proguard rules
- Update Libraw/Libraw-CMake

2.0.3
- Removed recycle from getBitmap().  Let me know if you feel it's necessary
- Added LibRaw.newInstance() factory to get the proper version of LibRaw (LibRaw or LibRaw26)
- For Android Q+, now creates RGB_888 (not RGBA_8888) and RGBA_F16 Bitmap.Config.Hardware Bitmaps.  Create a new LibRaw() directly if you don't want Hardware bitmaps for some reason.

2.0.2
- Fix rotation issues
- Add cancel functions

2.0.1
- Change getBitmap\[16\]() to remove intermediate step that creates an RGB memory image.  Now directly creates the Bitmap from the image\[\] data.
- Add methods setCaptureScaleMul(), getColorCurve() and dcrawProcessForce(colorCurve) to force consistent white balance in future runs.

2.0.0
- Moved from static LibRaw to instance.  This allows multiple LibRaw instances to exist at the same time.
