## Android Reversing

###### Android Application packaging formats :-
* APK
* AAR

###### Tools for reversing
* aapt
* dex2jar
* apktool
* Androguard

###### Rename the APK to ZIP
![Alt text](https://github.com/Kan1shka9/AndroidScratch/blob/master/images/1.PNG)

###### Anatomy
* <i>AndroidManifest.xml</i>	-> Manifest file in binary XML format
* <i>classes.dex</i>	-> application code compiled into dex format
* <i>resources.arsc</i> -> application resources precompiles in binary XML format
* <i>res/</i> -> folder contains resources not compiled into resources.arsc
<br>![Alt text](https://github.com/Kan1shka9/AndroidScratch/blob/master/images/2.PNG)
* <i>lib/</i> -> folder containing compiled code
<br>![Alt text](https://github.com/Kan1shka9/AndroidScratch/blob/master/images/3.PNG)
* <i>META-INF/</i> ->
<br>![Alt text](https://github.com/Kan1shka9/AndroidScratch/blob/master/images/4.PNG)
  * MANIFEST.MF -> Stores metadata about the contents of the JAR
  * CERT.RSA -> Certificate of the application
  * CERT.SF -> Contains the list of resources and SHA-1 digest of the corresponding lines in the MANIFEST.MF file
