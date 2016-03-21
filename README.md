## Android Reversing

###### Android application packaging formats :-
* APK
* AAR

###### Tools for reversing :-
* aapt
* dex2jar
* apktool
* Androguard

##### APK

###### Rename the APK to ZIP :-
![Alt text](https://github.com/Kan1shka9/AndroidScratch/blob/master/images/1.PNG)

###### Anatomy :-
* <b><i>AndroidManifest.xml</i></b>	-> Manifest file in binary XML format which specifies permissions
* <b><i>classes.dex</i></b>	-> application code compiled into dex format
* <b><i>resources.arsc</i></b> -> application resources precompiles in binary XML format
* <b><i>res/</i></b> -> folder contains resources not compiled into resources.arsc
<br>![Alt text](https://github.com/Kan1shka9/AndroidScratch/blob/master/images/2.PNG)
* <b><i>lib/</i></b> -> folder containing compiled code
<br>![Alt text](https://github.com/Kan1shka9/AndroidScratch/blob/master/images/3.PNG)
* <b><i>META-INF/</i></b> ->
<br>![Alt text](https://github.com/Kan1shka9/AndroidScratch/blob/master/images/4.PNG)
  * MANIFEST.MF -> Stores metadata about the contents of the JAR
  * CERT.RSA -> Certificate of the application
  * CERT.SF -> Contains the list of resources and SHA-1 digest of the corresponding lines in the MANIFEST.MF file
* <b><i>assets/</i></b>	-> [optional folder] Contains applications assets which can be retrieved by AssetManager.

###### DEX (dalvik executable) :-
- Complied code which can be interpreted by Dalvik virtual machine or Android Runtime (ART).
- .java --(javac)--> .class --(dx)--> class.dex
```
and@PT:~/android-sdk-linux/build-tools/23.0.2$ file dx
dx: Bourne-Again shell script, ASCII text executable
```

###### Obtaining the APK file :-
* Pre installed applications
  * Location -> /system/app
<br>![Alt text](https://github.com/Kan1shka9/AndroidScratch/blob/master/images/5.PNG)
* User installed applications
  * Location -> /data/app
<br>![Alt text](https://github.com/Kan1shka9/AndroidScratch/blob/master/images/6.PNG)
* Get the APK from the device
 * List available packages -> <i>./adb shell pm list packages -f</i>
  <br>![Alt text](https://github.com/Kan1shka9/AndroidScratch/blob/master/images/7.PNG)
 * Get the apk -> <i>./adb pull -p /data/app/org.owasp.goatdroid.fourgoats-1.apk output.apk</i>
  <br>![Alt text](https://github.com/Kan1shka9/AndroidScratch/blob/master/images/8.PNG)

##### AAR
Binary distribution of an android library project

###### Rename the AAR to ZIP :-
![Alt text](https://github.com/Kan1shka9/AndroidScratch/blob/master/images/9.PNG)

###### Anatomy :-
* <b><i>AndroidManifest.xml</i></b>	-> Manifest file in plain XML format
* <b><i>classes.jar</i></b> -> Java classes of the library
* <b><i>res/</i></b>	-> Contains resources used by the library
* <b><i>R.txt</i></b> -> Output of aapt with --output-text-symbols. List of all resources referenced by the library
* <b><i>assets/</i></b> -> [optional folder] Contains assets used by the libraries
* <b><i>libs/*.jar</i></b>	-> [optional folder] Contains external libraries
* <b><i>jni//*.so</i></b> -> [optional folder] Contains native libraries
* <b><i>proguard.txt</i></b> -> [optional file]	Proguard configuration file.
* <b><i>lint.jar</i></b> ->	[optional file]	Custom Lint rules.
