react-native-audio-toolkit
==========================

This is a cross-platform audio library for React Native. Both audio playback
and recording is supported, but for now only very basic functionality has been
implemented.

How to get this stuff running?
------------------------------

Expecting you have the React Native development environment in place, are
starting with a React Native hello world project and have managed to run it on
an actual Android/iOS device:

* Install library via npm

    ```
    npm install --save react-native-audio-toolkit
    ```

### Android

1. Append dependency to end of `android/settings.gradle` file

    ```
    ...

    include ':react-native-audio-toolkit'
    project(':react-native-audio-toolkit').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-audio-toolkit/android/player')
    ```

2. Add dependency to `android/app/build.gradle`

    ```
    ...

    dependencies {
        ...
        compile project(':react-native-audio-toolkit')
    }
    ```

3. Register the module in `android/app/src/main/java/com/<project>/MainActivity.java`

    ```
    package com.<project>;

    import com.facebook.react.ReactActivity;
    import com.facebook.react.ReactPackage;
    import com.facebook.react.shell.MainReactPackage;

    import com.futurice.AudioPackage; // <------------------------ here

    ...

    protected List<ReactPackage> getPackages() {
        return Arrays.<ReactPackage>asList(
            ...
            new MainReactPackage(), new AudioPackage() // <------- here
        );
    }
    ```

4. (optional) If you wish to record audio, add the following permissions to
   `android/app/src/main/AndroidManifest.xml`

    ```
    <manifest ...>

        <uses-permission android:name="android.permission.RECORD_AUDIO" />
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
        ...

    </manifest>
    ```

    This is to get permissions for recording audio and writing to external storage.

    TODO: Android 6.0 permissions model once supported by React Native:
    https://facebook.github.io/react-native/docs/known-issues.html#android-m-permissions


### iOS

TODO


### Example app

#### `index.android.js`

```
TODO
```

#### `index.ios.js`

```
TODO
```

#### `index.js`

```
TODO
```

### Run the app

```
adb reverse tcp:8081 tcp:8081
react-native run-android
```

Then start clicking the buttons, it should be quite simple.

Media events
------------

The project aims to follows
[HTML5 <audio> tag](https://developer.mozilla.org/en/docs/Web/Guide/Events/Media_events)
conventions as close as possible, however because React Native events are global,
the events are prefixed with `RCTAudioPlayer` and `RCTAudioRecorder` accordingly:

NOTE: [Media events documentation](https://developer.mozilla.org/en/docs/Web/Guide/Events/Media_events) by
Mozilla Contributors is licensed under [CC-BY-SA 2.5](http://creativecommons.org/licenses/by-sa/2.5/):

### RCTAudioPlayer events

Event name                   | Description
-----------------------------|------------------------
`RCTAudioPlayer:playing`     | Sent when the media begins to play (either for the first time, after having been paused, or after ending and then restarting).
`RCTAudioPlayer:play`        | Sent when playback of the media starts after having been paused; that is, when playback is resumed after a prior *pause* event.
`RCTAudioPlayer:pause`       | Sent when playback is paused.
`RCTAudioPlayer:ended`       | Sent when playback completes.
`RCTAudioPlayer:error`       | Sent when an error occurs. The event handler is passed a string with a reason.
`RCTAudioPlayer:info`        | TODO: https://developer.android.com/reference/android/media/MediaPlayer.OnInfoListener.html

### RCTAudioRecorder events

Event name                   | Description
-----------------------------|------------------------
`RCTAudioPlayer:start`       | Sent when recording starts.
`RCTAudioPlayer:pause`       | Sent when recording is paused. (TODO: implement)
`RCTAudioPlayer:ended`       | Sent when recording completes.
`RCTAudioPlayer:error`       | Sent when an error occurs. The event handler is passed a string with a reason.
`RCTAudioPlayer:info`        | TODO: https://developer.android.com/reference/android/media/MediaRecorder.OnInfoListener.html

License
-------

All Java code here licensed under MIT license, see LICENSE file. Some of the
files are from React Native templates and are licensed accordingly.