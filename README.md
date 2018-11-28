# Oculus-Go-Unity-
Walk-through to publishing an app on Oculus Go via Unity. 

## What You’ll Need

1.	Unity 3D
2.	Andriod Studio
3.	A computer with decent graphics card
4.	An Oculus Go!

## 1.	Download and Install Unity 
-	Install latest [Unity](https://unity3d.com/get-unity/download/archive).
-	 When Installing make sure to add on Andriod Build support

## 2.	Download and Install [Android Studio](https://developer.android.com/studio/) .

## 3.	Grab Oculus Core Utilities for Unity [Oculus Core Utilities](https://developer.oculus.com/downloads/unity/)
## 4.	Android Development Software Setup
-	Open Android Studio 
-	On the welcome screen, click ###Configure on the bottom right, and then the ###SDK Manager 
![Andriod Studio Image](https://cdn-images-1.medium.com/max/1400/1*Iuxvu3UVvkXmX4jdKW8VHw.png)
-	Under the SDK Platforms tab, make sure API Levels 21 through 27 are checked.

-	On the SDK Tools tab, check the box next to Show Package Details in the lower right corner of the window.

-	Under Android SDK Build-Tools 28-rc2, make sure the highest numbered item is check that does not end with “-rc1” or “-rc2”. As of this writing, that is 27.0.3.

![Andriod SDK build tools](https://cdn-images-1.medium.com/max/800/1*6dwO0ZaePdAx8IAzOsf7mA.png)

-	Also under SDK Tools make sure the follow are checked:

1-	LLDB
2-	Andriod SDK Platform-Tools
3-	Andriod SDK Tools 25.2.5
4-	NDK

-	Click ###Apply. This will install everything you selected above on the SDK tabs.
-	Back on the welcome screen, click ###Configure on the bottom right, and then ###Project Defaults > ###Project Structure
-	Here you’ll the file paths for the SDK, JDK and NDK. Copy these down in a text editor; we’ll need these shortly
https://cdn-images-1.medium.com/max/1200/1*563lDaV1n6KiTjwcVBoLPg.png 

-	Set your “environment variables”:
-	On your Windows machine, search for “Environment Variables”. This should take you to Control Panel > System Properties. Go to the Advanced Tab, then to the Environment Variables button in the lower right.
-	In the top section, set/modify/add the following variables:
Set the environment variable JAVA_HOME to the JDK location.
Set the environment variable ANDROID_HOME to the Android SDK location.
Set the environment variable ANDROID_NDK_HOME to the Android NDK location.
Add the JDK tools directory to your PATH, ie C:\Program Files\Android Studio\jre\bin

-	One of the errors I kept running into when building for Android in Unity was “Unable to list target platforms”. It’s vague and frustrating. Here’s how to fix it [stackoverflow post]( https://stackoverflow.com/questions/42538433/not-finding-android-sdk-unity#)
Delete android sdk “tools” folder : [Your Android SDK root]/tools -> tools
Download SDK Tools: http://dl-ssl.google.com/android/repository/tools_r25.2.5-windows.zip
Extract that to Android SDK root

## 5-	Setting Up Unity to Build for Andrioid 

Open Unity and create a new project
Once your new (or existing) project opens, we need to set it to build for Android.
Go to File > Build Settings
Select Android and then Switch Platform. (If you did not add Android support when you first installed Unity, you will have to do so now, then restart Unity). 

![Build Settings Example](https://cdn-images-1.medium.com/max/1000/1*lPGanaP_pgO_Kwc3PQb9YQ.png )

-	Close the Build Settings window.
-	Go to Edit > Preferences
-	Click on the External Tools tab
-	Scroll down to the Android section
-	Set the SDK, JDK and NDK paths to what you copied to the text file in Step 4.
-	Close the Preferences window.
-	Go to Edit > Project Settings > Player
-	Scroll down to XR Settings. Click the box next to Virtual Reality Supported.

![XR Settings](https://cdn-images-1.medium.com/max/800/1*EsjEHBCHTDVB7lGSVrVo6A.png)

-	Verify that Oculus appears in the SDK’s list. If not, click the “+” to the right, and select Oculus.
-	Scroll back up to the top and set your Company Name and Product Name.
-	Then scroll down to Other . Set the Package Name field to com.[CompanyName].[ProductName]
-	For Minimum API Level — I would set this API Level 21

## 6) Import Oculus Samples Scenes

To get started with your app, we’ll import some premade sample scenes that Oculus was nice enough to make for us.

-	Grab the OculusUtilities Unity package that you downloaded in step 3
-	Drag and drop OculusUtilities.unity into the Asset folders of your project, in the Unity window. Import when prompted.
-	Now, in your Assets folder, go to Oculus > VR > Scenes. Double click GearVrControllerTest.
-	In the hierarchy of the scene, dive down within the OVRCameraRig object to find the OculusGoControllerModel within the scene. Double click it to focus on it in the scene view (see below).
![moreIMages](https://cdn-images-1.medium.com/max/800/1*x83k91yw2TfkuS0oG6-t4A.png)

## 7) Enable Developer Mode on the Go
(Taken from the Oculus Developer documentation)

To begin development locally for Oculus Go, you must enable Developer Mode in the companion app. Before you can put your device in Developer Mode, you need to have created (or belong to) a developer organization on the Oculus Dashboard.

To join an existing organization:

You’ll need to request access to the existing Organization from the admin.
You’ll receive an email invite. Once accepted, you’ll be a member of the Organization.
To create a new organization:

Go to: https://dashboard.oculus.com/organization/create
Fill in the appropriate information.
Enable Developer Mode
To put your Oculus Go in developer mode:

Open the Oculus app on your mobile device.
In the Settings menu, select your Oculus Go headset that you’re using for development.
Select More Settings.
Toggle Developer Mode on.
8) Set up Android Debug Bridge
We’re almost there (I promise)! Before we can actually move our Unity app from our computer to our Go, we need to install Android Debug Bridge (ADB) and the drivers for the Oculus Go.

Download and install the Oculus Go ADB driver:
Download the zip file containing the driver.
Unzip the file.
Right-click on the .inf file and select Install.
Download and install [ADB](https://forum.xda-developers.com/showthread.php?t=2588979) 

See steps starting at 5:40 mark in video below

https://www.youtube.com/watch?v=baWEzvLC8Bo

## 9) Connect your Go and Build!
Connect your go to your PC via micro-USB.
In the ADB window from the last step, run adb devices to confirm that your Go has been detected.
Back in Unity, go to File > Build Settings
Click “Add Open Scenes”, and ensure only the scene GearVrControllerTest has the check mark next to it checked.
Click Build

![build](https://cdn-images-1.medium.com/max/800/1*l5D5Khe-a3IVljkOZnd37A.png)

-	Select the folder where you would like to place the .APK file that’s generated. I like to create a “Builds” folder in the project. Save.
-	After the .APK is generated, navigate to it in File Explorer. Copy it to the same directory where you installed ADB in Step 8.
-	Being the ADB window back up.
-	Run adb install [NameOfYourApp].apk
-	You should now see the file get transferred to your Oculus Go. In a minute or two, it should then show the message Success.
-	Congrats — you did it!!
-	Now, to run your app, put on your Go and go to Library > Unknown Sources. You should see the Bundle ID of your app on the last page of the Unknown Apps list. Click on it to launch it, and enjoy!
-	To uninstall run adb uninstall *package name*. For example, adb uninstall com.headjack.myapp.
