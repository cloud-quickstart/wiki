# Android Development
## Add Google Pixel 6 and Pixel 6 pro to Android Studio
https://developer.android.com/studio/run/device

## Add Google Pixel Watch to Android Studio

- https://developer.android.com/training/wearables/get-started/creating
- https://play.google.com/store/apps/details?id=com.google.android.wearable.app
On the watch turn off ADB debugging, selecte wireless debugging, pair with the code on the android studio side over wifi

<img width="619" alt="Screen Shot 2022-11-07 at 20 42 30" src="https://user-images.githubusercontent.com/24765473/200453424-574d8b9f-7619-452e-a70e-20b2569237ec.png">

See new pixel watch on the Device Manager under the Physical tab
<img width="1388" alt="Screen Shot 2022-11-07 at 20 45 17" src="https://user-images.githubusercontent.com/24765473/200453520-8dbbc66c-4796-497f-ac9a-d980d0549fc2.png">

## Setup Android Studio
### JDK
### Gradele
```
An exception occurred applying plugin request [id: 'com.android.application']
> Failed to apply plugin 'com.android.internal.version-check'.
   > Minimum supported Gradle version is 7.5. Current version is 7.4. If using the gradle wrapper, try editing the distributionUrl in /Users/michaelobrien/wse_github/ObrienlabsDev/biometric-android-app/gradle/wrapper/gradle-wrapper.properties to gradle-7.5-all.zip

```
fix
https://docs.gradle.org/current/userguide/installation.html
```
brew install gradle
```

## Sensors
https://developer.android.com/guide/topics/sensors/sensors_overview#sensors-practices


```
        for (s in (getSystemService(SENSOR_SERVICE) as SensorManager).getSensorList(Sensor.TYPE_ALL))
            Log.d("Sensor:", s.name)
            
---------------------------- PROCESS STARTED (31729) for package dev.obrienlabs.biometric.android ----------------------------
2023-04-23 23:33:46.981 31729-31729 Sensor:                 pid-31729                            D  lsm6dso LSM6DSO Accelerometer Non-wakeup
2023-04-23 23:34:05.746 31729-31729 Sensor:                 pid-31729                            D  AK09918 Magnetometer
2023-04-23 23:34:08.835 31729-31729 Sensor:                 pid-31729                            D  lsm6dso LSM6DSO Gyroscope Non-wakeup
2023-04-23 23:34:10.580 31729-31729 Sensor:                 pid-31729                            D  STK33915 Light Ambient Light Sensor Non-wakeup
2023-04-23 23:34:12.336 31729-31729 Sensor:                 pid-31729                            D  lps22hh Pressure Sensor Non-wakeup
2023-04-23 23:34:15.116 31729-31729 Sensor:                 pid-31729                            D  gravity  Non-wakeup
2023-04-23 23:34:17.008 31729-31729 Sensor:                 pid-31729                            D  linear_acceleration
2023-04-23 23:34:18.546 31729-31729 Sensor:                 pid-31729                            D  Rotation Vector  Non-wakeup
2023-04-23 23:34:20.539 31729-31729 Sensor:                 pid-31729                            D  AK09918 Magnetometer-Uncalibrated
2023-04-23 23:34:22.276 31729-31729 Sensor:                 pid-31729                            D  Game Rotation Vector  Non-wakeup
2023-04-23 23:34:25.398 31729-31729 Sensor:                 pid-31729                            D  lsm6dso LSM6DSO Gyroscope-Uncalibrated Non-wakeup
2023-04-23 23:34:27.921 31729-31729 Sensor:                 pid-31729                            D  smd  Wakeup
2023-04-23 23:34:29.548 31729-31729 Sensor:                 pid-31729                            D  step_detector  Non-wakeup
2023-04-23 23:34:31.029 31729-31729 Sensor:                 pid-31729                            D  step_counter  Non-wakeup
2023-04-23 23:34:32.452 31729-31729 Sensor:                 pid-31729                            D  Tilt Detector  Wakeup
2023-04-23 23:35:02.243 31729-31729 Sensor:                 pid-31729                            D  Pick Up Gesture  Wakeup
2023-04-23 23:35:26.147 31729-31729 Sensor:                 pid-31729                            D  auto_rotation Screen Orientation Sensor Non-wakeup
2023-04-23 23:35:34.319  1596-4652  sensors-hal             pid-1596                             I  ssc_conn_event_cb:875, event[0] sensor:smd  Wakeup, msg_id=1025, ts=11885227373785
2023-04-23 23:36:02.759  1596-3706  sensors-hal             pid-1596                             I  ssc_conn_event_cb:875, event[0] sensor:slocationcore  Wakeup, msg_id=1025, ts=11885773434019
2023-04-23 23:36:02.760  1596-3706  sensors-hal             pid-1596                             I  ssc_conn_event_cb:875, event[0] sensor:slocationcore  Wakeup, msg_id=1025, ts=11885773434299
2023-04-23 23:36:02.761  1596-3706  sensors-hal             pid-1596                             I  ssc_conn_event_cb:875, event[0] sensor:slocationcore  Wakeup, msg_id=1025, ts=11885773434539
2023-04-23 23:36:20.794 31729-31729 Sensor:                 pid-31729                            D  motion_detect
2023-04-23 23:36:24.270 31729-31729 Sensor:                 pid-31729                            D  lsm6dso LSM6DSO Accelerometer-Uncalibrated Non-wakeup
2023-04-23 23:36:33.875 31729-31729 Sensor:                 pid-31729                            D  STK33915 Light CCT WideIR ALS Non-wakeup
2023-04-23 23:36:38.552 31729-31729 Sensor:                 pid-31729                            D  interrupt_gyro  Non-wakeup
2023-04-23 23:36:44.057 31729-31729 Sensor:                 pid-31729                            D  STK33915 Proximity Strm Proximity strm Non-wakeup
2023-04-23 23:36:46.652 31729-31729 Sensor:                 pid-31729                            D  SensorHub type
2023-04-23 23:36:48.761 31729-31729 Sensor:                 pid-31729                            D  STK33915 Light CCT  Non-wakeup
2023-04-23 23:36:50.473 31729-31729 Sensor:                 pid-31729                            D  Wake Up Motion  Wakeup
2023-04-23 23:36:52.812 31729-31729 Sensor:                 pid-31729                            D  STK33915 Proximity Proximity Sensor Wakeup
2023-04-23 23:36:54.761 31729-31729 Sensor:                 pid-31729                            D  call_gesture  Wakeup
2023-04-23 23:36:56.375 31729-31729 Sensor:                 pid-31729                            D  STK33915 Auto Brightness Auto Brightness Non-wakeup
2023-04-23 23:36:57.643 31729-31729 Sensor:                 pid-31729                            D  Pocket mode  Wakeup
2023-04-23 23:36:58.937 31729-31729 Sensor:                 pid-31729                            D  Led Cover Event  Wakeup
2023-04-23 23:37:00.218 31729-31729 Sensor:                 pid-31729                            D  Light seamless  Wakeup
2023-04-23 23:37:01.674 31729-31729 Sensor:                 pid-31729                            D  Flip Cover Detector  Wakeup
2023-04-23 23:37:03.140 31729-31729 Sensor:                 pid-31729                            D  Sar BackOff Motion  Wakeup
2023-04-23 23:37:04.360 31729-31729 Sensor:                 pid-31729                            D  Drop Classifier  Wakeup
2023-04-23 23:37:05.641 31729-31729 Sensor:                 pid-31729                            D  Pocket Position Mode  Wakeup
2023-04-23 23:37:07.640 31729-31729 Sensor:                 pid-31729                            D  TSL2585 Rear ALS
2023-04-23 23:37:09.097 31729-31729 Sensor:                 pid-31729                            D  Touch Proximity Sensor
2023-04-23 23:37:10.876 31729-31729 Sensor:                 pid-31729                            D  Hall IC
2023-04-23 23:37:12.074 31729-31729 Sensor:                 pid-31729                            D  Palm Proximity Sensor version 2
2023-04-23 23:37:13.213 31729-31729 Sensor:                 pid-31729                            D  Motion Sensor
2023-04-23 23:37:14.379 31729-31729 Sensor:                 pid-31729                            D  Orientation Sensor
---------------------------- PROCESS ENDED (31729) for package dev.obrienlabs.biometric.android ----------------------------
```

## Android related Languages
- Java
- React Native
- Flutter
- Go
- Kotlin
- 
