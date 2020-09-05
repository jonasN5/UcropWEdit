## uCrop'n'Edit - Image Cropping + Editing Library for Android

#### Using the source code of "<a href="https://github.com/Yalantis/uCrop">uCrop</a>", I’ve added four new features - ability to change Brightness, Contrast, Saturation and Sharpness.

<p align="center" style="background-color:#ededed">
  <img src="preview.gif" width="320" height="560">
</p>

## Usage

1. Include the library as local library project.

	```
	allprojects {
	   repositories {
	      jcenter()
	      maven { url "https://jitpack.io" }
	   }
	}
	```


    ``` implementation 'com.github.yalantis:ucrop:2.2.3' ``` - lightweight general solution 
    
    ``` implementation 'com.github.yalantis:ucrop:2.2.3-native' ``` - get power of the native code to preserve image quality (+ about 1.5 MB to an apk size)
    
2. Add UCropActivity into your AndroidManifest.xml

    ```
    <activity
        android:name="com.yalantis.ucrop.UCropActivity"
        android:screenOrientation="portrait"
        android:theme="@style/Theme.AppCompat.Light.NoActionBar"/>
    ```

3. The uCrop configuration is created using the builder pattern.

	```java
    UCrop.of(sourceUri, destinationUri)
        .withAspectRatio(16, 9)
        .withMaxResultSize(maxWidth, maxHeight)
        .start(context);
    ```


4. Override `onActivityResult` method and handle uCrop result.

    ```java
    @Override
    public void onActivityResult(int requestCode, int resultCode, Intent data) {
        if (resultCode == RESULT_OK && requestCode == UCrop.REQUEST_CROP) {
            final Uri resultUri = UCrop.getOutput(data);
        } else if (resultCode == UCrop.RESULT_ERROR) {
            final Throwable cropError = UCrop.getError(data);
        }
    }
    ```
5. You may want to add this to your PROGUARD config:

    ```
    -dontwarn com.yalantis.ucrop**
    -keep class com.yalantis.ucrop** { *; }
    -keep interface com.yalantis.ucrop** { *; }
    ```

# Customization

If you want to let your users choose crop ratio dynamically, just do not call `withAspectRatio(x, y)`.

uCrop builder class has method `withOptions(UCrop.Options options)` which extends library configurations.

Currently you can change:

   * image compression format (e.g. PNG, JPEG, WEBP), compression
   * image compression quality [0 - 100]. PNG which is lossless, will ignore the quality setting.
   * whether all gestures are enabled simultaneously
   * maximum size for Bitmap that is decoded from source Uri and used within crop view. If you want to override default behaviour.
   * toggle whether to show crop frame/guidelines
   * setup color/width/count of crop frame/rows/columns
   * choose whether you want rectangle or oval crop area
   * the UI colors (Toolbar, StatusBar, active widget state)
   * and more...
    
# Compatibility
  
  * Library - Android ICS 4.0+ (API 14) (Android GINGERBREAD 2.3+ (API 10) for versions <= 1.3.2)
  * Sample - Android ICS 4.0+ (API 14)
  * CPU - armeabi armeabi-v7a x86 x86_64 arm64-v8a (for versions >= 2.1.2)
  
# Changelog
### Version: 2.2.3

  * Several fixes including [#445](https://github.com/Yalantis/uCrop/issues/445), [#465](https://github.com/Yalantis/uCrop/issues/465) and more!    
  * Material design support 
  * uCrop fragment as child fragment
  * Added Italian language

### Version: 2.2.2

* uCrop fragment added
* bugfix

### Version: 2.2.1

    ``` implementation 'com.github.krokyze:ucropnedit:2.2.6' ```
    
2. To use uCrop’n’Edit, you can follow the exact same methods as for uCrop: <a href="https://github.com/Yalantis/uCrop#usage">Usage</a>

If you have any interesting ideas for uCrop’n’Edit do not be afraid to let me know. You can easily leave a request and I will be happy to take a look at the viability of your proposal. I’ll be more than happy to try and add some new features to the library, if I think they can make it even better!


#### Please keep in mind that most of the work is developed by Yalantis, so if you find any bugs that’s not related to brightness, contrast, saturation or sharpness, you should add a new issue to their <a href="https://github.com/Yalantis/uCrop/issues">Github page</a> and as they will push update, I will pull it to make sure everything works as best as it can.

Massive thanks to guys from Yalantis for open sourcing this great library!

## Changelog (<a href="https://github.com/Yalantis/uCrop#changelog">uCrop Changelog</a>)

### Version 2.2.6 (based on uCrop 2.2.6)

  * Merged new version from uCrop.

### Version 2.2.5 (based on uCrop 2.2.4)

  * Merged new version from uCrop.

### Version 2.2.4 (based on uCrop 2.2.3)

  * Merged new version from uCrop.

### Version 2.2.3 (based on uCrop 2.2.2)

  * Merged new version from uCrop.

### Version 2.2.2 (based on uCrop 2.2.1)

  * Saturation feature
  * Sharpness feature (supported for devices with >= API 17)

### Version: 2.2.1

  * Brightness feature
  * Contrast feature

## License

    Copyright 2017, Yalantis

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
