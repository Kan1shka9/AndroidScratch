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
* <b><i>AndroidManifest.xml</i></b>	- Manifest file in binary XML format which specifies permissions
* <b><i>classes.dex</i></b>	- application code compiled into dex format
* <b><i>resources.arsc</i></b> - application resources precompiles in binary XML format
* <b><i>res/</i></b> - folder contains resources not compiled into resources.arsc
<br>![Alt text](https://github.com/Kan1shka9/AndroidScratch/blob/master/images/2.PNG)
* <b><i>lib/</i></b> - folder containing compiled code
<br>![Alt text](https://github.com/Kan1shka9/AndroidScratch/blob/master/images/3.PNG)
* <b><i>META-INF/</i></b> -
<br>![Alt text](https://github.com/Kan1shka9/AndroidScratch/blob/master/images/4.PNG)
  * MANIFEST.MF - Stores metadata about the contents of the JAR
  * CERT.RSA - Certificate of the application
  * CERT.SF - Contains the list of resources and SHA-1 digest of the corresponding lines in the MANIFEST.MF file
* <b><i>assets/</i></b>	- [optional folder] Contains applications assets which can be retrieved by AssetManager.

###### DEX (dalvik executable) :-
- Complied code which can be interpreted by Dalvik virtual machine or Android Runtime (ART).
- .java --(javac)-- .class --(dx)-- class.dex
```
and@PT:~/android-sdk-linux/build-tools/23.0.2$ file dx
dx: Bourne-Again shell script, ASCII text executable
```

###### Obtaining the APK file :-
* Pre installed applications
  * Location - /system/app
<br>![Alt text](https://github.com/Kan1shka9/AndroidScratch/blob/master/images/5.PNG)
* User installed applications
  * Location - /data/app
<br>![Alt text](https://github.com/Kan1shka9/AndroidScratch/blob/master/images/6.PNG)
* Get the APK from the device
 * List available packages - <br>```./adb shell pm list packages -f```
  <br>![Alt text](https://github.com/Kan1shka9/AndroidScratch/blob/master/images/7.PNG)
 * Get the apk - <br>```./adb pull -p /data/app/org.owasp.goatdroid.fourgoats-1.apk output.apk```
  <br>![Alt text](https://github.com/Kan1shka9/AndroidScratch/blob/master/images/8.PNG)

##### AAR
Binary distribution of an android library project

###### Rename the AAR to ZIP :-
![Alt text](https://github.com/Kan1shka9/AndroidScratch/blob/master/images/9.PNG)

###### Anatomy :-
* <b><i>AndroidManifest.xml</i></b>	- Manifest file in plain XML format
* <b><i>classes.jar</i></b> - Java classes of the library
* <b><i>res/</i></b>	- Contains resources used by the library
* <b><i>R.txt</i></b> - Output of aapt with --output-text-symbols. List of all resources referenced by the library
* <b><i>assets/</i></b> - [optional folder] Contains assets used by the libraries
* <b><i>libs/*.jar</i></b>	- [optional folder] Contains external libraries
* <b><i>jni//*.so</i></b> - [optional folder] Contains native libraries
* <b><i>proguard.txt</i></b> - [optional file]	Proguard configuration file.
* <b><i>lint.jar</i></b> -	[optional file]	Custom Lint rules.

##### AAPT - Android Asset Packaging Tool
* Used to compile resources into binary assets.
* Allows you to view, create, and update Zip-compatible archives (zip, jar, apk)
* Used to extract information from the APK

###### Contents of APK file :-
```./aapt list -v diva-beta.apk```
<br>
![Alt text](https://github.com/Kan1shka9/AndroidScratch/blob/master/images/10.PNG)

###### Obtain more details :-
```./aapt dump badging diva-beta.apk```
<br>
![Alt text](https://github.com/Kan1shka9/AndroidScratch/blob/master/images/11.PNG)

###### Extract explicit permissions :-
```./aapt dump permissions diva-beta.apk```
![Alt text](https://github.com/Kan1shka9/AndroidScratch/blob/master/images/12.PNG)

###### Extract configurations in the APK file :-
```./aapt dump configurations diva-beta.apk```
![Alt text](https://github.com/Kan1shka9/AndroidScratch/blob/master/images/13.PNG)

###### Extract resource table from the APK file :-
```./aapt dump resources diva-beta.apk```
![Alt text](https://github.com/Kan1shka9/AndroidScratch/blob/master/images/14.PNG)

###### View the AndroidManifest.xml :-
```./aapt dump xmltree diva-beta.apk AndroidManifest.xml```
![Alt text](https://github.com/Kan1shka9/AndroidScratch/blob/master/images/15.PNG)

##### dex2jar
* Java decompiler
* Used to convert class files to jar files
<br>
```./d2j-dex2jar.sh -f -o class.jar diva-beta.apk```
![Alt text](https://github.com/Kan1shka9/AndroidScratch/blob/master/images/16.PNG)

###### View the pseudo source code using JD-GUI :-
```java -jar jd-gui-1.4.0.jar dex2jar-2.0/class.jar```
<br>
![Alt text](https://github.com/Kan1shka9/AndroidScratch/blob/master/images/17.PNG)

###### Convert JAR back to DEX :-
```./d2j-jar2dex.sh -f -o class.dex class.jar```
<br>
![Alt text](https://github.com/Kan1shka9/AndroidScratch/blob/master/images/18.PNG)

###### Limitation
APK is a ZIP file so the files can be repackaged
We have to sign it with jarsigner to regenerate MANIFEST.MF
But a new APK can't be released as an update to the original as we do not have access to the keystore and private key
While performing an update the the system compares the certificate in the new version with that of the existing version

###### SMALI
Converts classes.dex to .smali files
<br>
```./d2j-dex2smali.sh diva-beta.apk```
<br>
![Alt text](https://github.com/Kan1shka9/AndroidScratch/blob/master/images/19.PNG)
![Alt text](https://github.com/Kan1shka9/AndroidScratch/blob/master/images/20.PNG)

##### apktool
* Decode the apk
<br>
![Alt text](https://github.com/Kan1shka9/AndroidScratch/blob/master/images/21.PNG)
  * apktool.yml - Contains info about the apk <br>
  ![Alt text](https://github.com/Kan1shka9/AndroidScratch/blob/master/images/22.PNG)
  * AndroidManifest.xml - Plain XML format
  ![Alt text](https://github.com/Kan1shka9/AndroidScratch/blob/master/images/23.PNG)
  * original/ - Files are directly copied from the apk <br>
  ![Alt text](https://github.com/Kan1shka9/AndroidScratch/blob/master/images/24.PNG)
  * smali/ - Contains the application source code in smali format
  * res/ - Contains the resources which are decoded

* Build the apk
<br>
![Alt text](https://github.com/Kan1shka9/AndroidScratch/blob/master/images/25.PNG)
