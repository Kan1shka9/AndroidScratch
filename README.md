## Android Reversing

###### Android application packaging formats :-
* APK
* AAR

###### Tools for reversing :-
* aapt
* dex2jar
* apktool
* Androguard

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

###### Location of APK file :-
* Pre installed applications
  * Location -> /system/app
<br>![Alt text](https://github.com/Kan1shka9/AndroidScratch/blob/master/images/5.PNG)
* User installed applications
  * Location -> /data/app
<br>![Alt text](https://github.com/Kan1shka9/AndroidScratch/blob/master/images/6.PNG)
