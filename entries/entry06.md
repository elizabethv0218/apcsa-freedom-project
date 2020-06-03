# Entry 6
##### 6/1/20

We are three months into quarantine, but that doesn't mean we have given up on our Freedom Project. Nadia, Aaliyah, and I are have been persisting in our efforts to make a functioning application.

Since my last blog entry, we've been creating the alarm. Nadia found a very useful video called [Java ( Android Studio ) - Notification App -](https://www.youtube.com/watch?v=44Nr3AT7fF4) that walked us through on what should be incorporated into the alarm. In our `activity_main.xml` file, we included elements in our layout like `EditText` (where the user can input a message like the name of their prescription), `TimePicker` (where the user can choose what time they would like to be reminded), and `Button` (the user can choose to set a new alarm or cancel an active one). In our `MainActivity.java` file, we applied the layout from its corresponding xml file and included code that would take in user inputs and create/cancel an alarm. Our `AlarmReceiver.java` file makes sure you are notified. At that point, we were on the **test and evaluate the prototype** step of the engineering design process. We conducted some trials to check that the alarm would go off and it did. However, when I tried to see if the alarm would go off at the same time everyday, I noticed the alarm-time would deviate from what was input. For example, when I set the alarm to go off at 1:20 PM, it did work in that afternoon, but the following days it would go off at 1:22 PM, 1:27 PM, 1:30 PM, 2:02 PM, 1:38 PM, 1:22 PM, and 1:48 PM (once per day). I notified my partners on this issue.

We were using the following line of code to have the alarm go off daily:
```
alarm.setRepeating(AlarmManager.RTC_WAKEUP, alarmStartTime, TimeUnit.MILLISECONDS.convert(1, TimeUnit.DAYS), alarmIntent);
```
We resorted to using sources like [this](https://stackoverflow.com/questions/25762505/send-notification-in-android) Stack Overflow thread but none have been successful.

As much as I wanted to test out potential solutions to this issue, I was forced to switch gears and study for my upcoming CollegeBoard AP Exams including the AP Computer Science A (APCSA) exam. After our APCSA exam, we transitioned back into working on our project. I opened the emulator and realized something was missing: the icon. We created a logo a while ago and almost forgot about it because we were concentrating on making the app viable.

![MedTrack](../images/logo1.png)

I used the video [Change The App Icon in Android Studio](https://www.youtube.com/watch?v=SDKwNh0TioE) to change our app icon. Some of the things I took away from the video were that our logo picture should be in png format (allows for transparency) and 512px by 512px. It was interesting to see that Android Studio automatically created different designs for the icon like a Google Play version, a round version, a rounded square version, etc. After a few adjustments, I ran the emulator, waited for the build gradle to successfully process, and the icon appeared in the app drawer.

We are now at the **improve as needed** stage of the engineering process. I moved on to creating a splash page for our app which is the first page users see before accessing the app itself. This tutorial [video](https://www.youtube.com/watch?v=JLIFqqnSNmg) was able to teach me how to remove the Action Bar, create animations with `translate` and `alpha`, and assign animations to specific layout elements as variables. I was relieved when this video taught me how to transition from the splash screen to the app itself. Unlike the CS50 IDE, every time you create a new java class, a corresponding xml file is created in Android Studio's IDE.

The first problem I encountered was figuring whether or not I should move the original code from `MainActivity.java` and `activity_main.xml` (about the alarm) into new java and xml files. The splash screen did work, but then nothing happened afterwards. I was afraid that doing so wouldn't work and that I'd have to go back to square one by undoing my edits. If there's anything that my experience in class and remote learning has taught me, it's that everything is worth a try. I was trying out the skill of **embracing failure**. I copied and pasted code related to the alarm page into new files I called `Dashboard.java` and `activity_dashboard.xml`. Of course I had to make a few changes like replacing any `MainActivity` with `Dashboard` to remove errors. The preview looked fine. It was the moment of truth. I ran the app and it worked just fine. Just to be sure, I set the alarm and it worked as well. My only pet peeve was that after the splash screen disappeared, the status bar would appear. It was getting late, so I told myself I'd do something about it in the morning.

That was a mistake.

I regret not having pushed my edits then because the next day I tried to remove the status bar. I was trying to follow a [guide](https://developer.android.com/training/system-ui/status) the Android Developer website had offered. I went into the `AndroidManifest.xml` file to work on it and when I tried it out, the emulator said that MedTrack was not responding. I deleted the code I added and tried again. Again the same message: MedTrack is not responding. I was starting to get worried because I hadn't touched anything else in the file. I performed `git checkout` on the file and the message still appeared. I went back to the video about the splash screen to check if I had accidentally deleted a piece of code, but the video did not touch the file. I was very confused. I replayed the video again using my **attention to detail** skills to see if the files `git status` says I edited were different from what I took away from the video. It was imperative I compare because the Android Studio IDE was saying that there were no errors. I got nothing.

I navigated myself to the 4: Run tab at the bottom. The tab records details about what you are doing in the emulator. When I ran the emulator, the Run tab looked fine until the text color turned red and said:
```
android.content.ActivityNotFoundException: Unable to find explicit activity class
```
The text in red went on and on. What I understood from it was that the activity class I wanted to proceed `MainActivity` was not being found. I googled this error and found solutions that were catered to specific issues related to this error. I could not find one that was similar to mine. The error message asked if I had declared the `Dashboard.java` class in `AndroidManifest.xml`. I did work in it that morning, but it was only three lines of code, nothing had contained `Dashboard` in it. I was confused because the night before I hadn't touched the file and it worked fine, but now it wasn't working. I looked at the structure of the `AndroidManifest.xml` file:
```java
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.medtrack">

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/AppTheme">
        <activity
            android:name=".MainActivity"
            android:label="@string/app_name"
            android:theme="@style/AppTheme.NoActionBar">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
        <receiver android:name=".AlarmReceiver" />
    </application>

</manifest>
```
I had to come up with my own solution. I first tried to use the `receiver` tags like the ones for `AlarmReceiver` to see if that would work. It didn't. Then I tried using the `activity` tags like the ones for `MainActivity`. It worked. I'm still very apprehensive about the whole ordeal because I think I would have noticed if I deleted a chunk of code. I'll admit defeat for now. Below is a video of how MedTrack works:

<video controls="true" allowfullscreen="true">
  <source src="../images/MedTrack-rec1.mov" type="video/mp4">
</video>

I can't say our MedTrack application is out of this world, but I am proud of everything I've learned by myself and with my partners these past couple of months. When we have the time, we will improve even further on our MVP. Considering the times we are going through, it's incredible we've come so far. Stay safe everyone.

[Previous](entry05.md) | [Next](entry07.md)

[Home](../README.md)