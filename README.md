# Android Login Form in Java
This Java Source Fixed By Me And It Now Workable I Just Updated Some function 

And Made A New Php FILE So It Have Some Trouble Like "An unknown error. Please contact the Modder" I Have Fixed This Errors So Now Enjoy The Source 

![](https://i.imgur.com/PNJEdzd.png)

# PHP

Add `login.php` to your server that supports PHP, use 000webhost.com for free webserver. Repo based hosting such as Github does not support PHP

Change URL on `public String sUrl` on `MainActivity.java` file

# Merging into your project

It's easy, just copy and paste the code into your project and make some changes

See the example folder how the login code was merged into the mod menu project on `MainActivity.java` file

# How to implement to APK:

**This is quite different to implement because the code depends on Activity, you can't just call static method via game's onCreate like `invoke-static {p0}, Luk/lgl/MainActivity;->Start(Landroid/content/Context;)V` so make sure you follow this steps**

First, know the game's launch activity/main activity

You can either use APK Easy Tool to view main activity like screenshot below:

![](https://i.imgur.com/JQdPjyZ.png)

Or decompile your **game APK** using apktool.jar, or any 3rd party CLI or GUI tools, and open `androidmanifest.xml` and search after `<action android:name="android.intent.action.MAIN"/>`

In this case, my game's main activity was `com.unity3d.player.UnityPlayerActivity`

![](https://i.imgur.com/FfOtc1K.png)

On Android Studio, put main activity of your game APK to `public String sGameActivity`

![](https://i.imgur.com/gstiBDk.png)

Build the project to APK file.

**Build** -> **Build Bundle(s)/APK(s)** -> **Build APK(s)**

If no errors occured, you did everything right and build will succeded. You will be notified that it build successfully

![](https://i.imgur.com/WpSKV1L.png)

Click on **locate** to show you the location of **build.apk**. It is stored at `(your-project)\app\build\outputs\apk\app-debug.apk`

![](https://i.imgur.com/wBTPSLi.png) 

Now decompile your **app-debug.apk**.

Copy your decompiled app-debug.apk smali to the game's smali folder. Example ours is com.example.loginform2, we would copy the `com` folder from `(app-debug\smali\com)` to the game's decompiled directory `(game name)\smali`. If the game have multidexes, add your smali to the last classes dex if possible to prevent compilation errors such as `Unsigned short value out of range: xxxxx`

On the game's `androidmanifest.xml`, besure that `<uses-permission android:name="android.permission.INTERNET"/>` exist

![](https://i.imgur.com/k0sLVUF.png)

Remove the `<action android:name="android.intent.action.MAIN"/>` like this:

![](https://i.imgur.com/z1RxPjc.png)

Near the end of application tag, add your new main activity above `</application>`. `com.example.loginform2.MainActivity` is your main activity

```xml
<activity android:configChanges="keyboardHidden|orientation|screenSize" android:name="com.example.loginform2.MainActivity" android:screenOrientation="portrait">
     <intent-filter>
         <action android:name="android.intent.action.MAIN"/>
         <category android:name="android.intent.category.LAUNCHER"/>
     </intent-filter>
</activity>
```

![](https://i.imgur.com/X4b8jBV.png)

Now compile the game APK

It should launch the login screen and successfully launch the activity after login :)

![](https://i.imgur.com/eyx8ldU.gif)

# Simple protection in lib

See `Main.cpp` for example how to check if the user has logged in

There are the codes called `Check()` and `loadLibrary`. They are commented out

You may need to protect your dex and lib files for that
