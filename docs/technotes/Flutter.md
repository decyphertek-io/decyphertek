Flutter
=====

Flutter modernizes the app development process and works on any screen. Integrates with Android Studio. 

Install
-------

     # if command fails, run as sudo
     sudo snap install flutter --classic
     sudo snap alias flutter.dart dart
     sudo snap install android-studio --classic
     android-studio
     flutter config --android-studio-dir /snap/android-studio/current/android-studio
     flutter config --android-sdk ~/Android/Sdk
     # Android SDK Command line tools
     > Android Studio > File > Settings > System Settings > Android SDK > SDK Tools > Select: Android SDK Command-Line Tools > Apply
     # You may need to restart any open editors for them to read new settings.
     flutter doctor --android-licenses
     flutter channel 
     # update Flutter to the latest dev branch revision
     flutter upgrade
     # enable Linux toolchain
     flutter config --enable-linux-desktop
     # enable macOS toolchain
     flutter config --enable-macos-desktop
     # enable Windows toolchain
     flutter config --enable-windows-desktop
     flutter doctor

Flutter Plugin
--------------

     1. Open plugin preferences (File > Settings > Plugins).
     2. Select Marketplace, select the Flutter plugin and click Install.

Create an Android App
---------------------

     1. Open the IDE and select New Flutter Project.
     2. Select Flutter, verify the Flutter SDK path with the SDK’s location. Then click Next.
     3. Enter a project name (for example, my_app).
     4. Select Application as the project type. Then click Next.
     5. Click Finish.
     6. Wait for Android Studio to create the project.

Run the Android app
-------------------

     1. Locate the main Android Studio toolbar: Main IntelliJ toolbar
     2. In the target selector, select an Android device for running the app. If none are listed as available, select Tools > AVD Manager and create one there. For details, see Managing AVDs.
     3. Click the run icon in the toolbar, or invoke the menu item Run > Run.

External Flutter Packages 
-------------------------

     flutter pub add english_words
     flutter pub get
     # add this line of code to /lib/main.dart
     import 'package:english_words/english_words.dart';

References
----------

     https://ubuntu.com/blog/getting-started-with-flutter-on-ubuntu
     https://docs.flutter.dev/get-started/install/linux
     https://docs.flutter.dev/get-started/test-drive
     https://docs.flutter.dev/get-started/codelab
