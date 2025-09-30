# Android Alarm Application with Service and BroadcastReceiver

This project is an Android application that demonstrates how to set, run, and cancel a one-time alarm using core Android components like `Service`, `BroadcastReceiver`, and `AlarmManager`.

## AIM

To create an Android application that allows a user to set a specific time for an alarm. When the alarm time is reached, a background `Service` is started, which plays an alarm sound. The user also has the ability to cancel a set alarm, which stops the sound if it's playing and prevents it from ringing in the future.

## Features

-   **Set Alarm**: Users can click a "Create" button to open a `TimePickerDialog` and select a time for the alarm.
-   **Display Set Time**: Once an alarm is set, its time is displayed on a dedicated card, which becomes visible.
-   **Alarm Notification**: At the exact time set by the user, an alarm sound starts playing.
-   **Cancel Alarm**: Users can cancel the scheduled alarm. If the alarm is already ringing, it will stop.
-   **Persistent Alarm Scheduling**: The app requests the necessary `SCHEDULE_EXACT_ALARM` permission to ensure reliability on modern Android versions.
-   **UI with Material Design**: The user interface is built using Material Components like `MaterialCardView` and `MaterialButton`.

### App Screenshots

<img width="435" height="892" alt="41" src="https://github.com/user-attachments/assets/29186a8e-c6f9-4b82-99bf-67bc5d4add03" />
<img width="448" height="898" alt="42" src="https://github.com/user-attachments/assets/e166b8d4-34d2-40a6-9f17-82b498e898d5" />
<img width="428" height="900" alt="43" src="https://github.com/user-attachments/assets/443aece4-d046-4727-b45f-cd4dfc9369f9" />





## Core Concepts Demonstrated

This project provides a practical study of several fundamental Android concepts:

-   **`Service`**: A background component used here as `AlarmService` to play the alarm sound independently of the app's UI. It uses `MediaPlayer` to manage the audio.
-   **`BroadcastReceiver`**: `AlarmBroadcastReceiver` listens for the alarm trigger from `AlarmManager`. It then starts the `AlarmService` to play the sound.
-   **`AlarmManager`**: The core Android class used to schedule and cancel time-based alarms that operate outside the lifecycle of the application. The project uses `setExact()` to ensure the alarm fires at the precise time.
-   **`PendingIntent`**: Wraps an `Intent` to be fired by `AlarmManager` at a later time, granting it permission to execute the `BroadcastReceiver` on the app's behalf.
-   **`TimePickerDialog`**: A standard dialog for a user-friendly time selection experience.
-   **`Calendar` & `SimpleDateFormat`**: Used to manage and format date and time information for setting the alarm and displaying it to the user.
-   **`MediaPlayer`**: Used within the `AlarmService` to play the raw alarm sound resource.
-   **Permissions**: The app properly declares `<uses-permission android:name="android.permission.SCHEDULE_EXACT_ALARM"/>` in the manifest and directs the user to system settings if the permission is not granted.
-   **Activity Lifecycle & UI Management**: Demonstrates managing UI visibility (`View.GONE`, `View.VISIBLE`) based on application state (e.g., showing the alarm card only when an alarm is set).

## Project Structure

-   **`MainActivity.kt`**: The main UI controller. It handles user interactions for creating and canceling alarms, displaying the `TimePickerDialog`, and communicating with the `AlarmManager`.
-   **`AlarmService.kt`**: A `Service` class that manages the `MediaPlayer` to play and stop the alarm sound. It is designed to be started and stopped by intents.
-   **`AlarmBroadcastReceiver.kt`**: A `BroadcastReceiver` that acts as the entry point for the `AlarmManager`. When triggered, it starts the `AlarmService`.
-   **`activity_main.xml`**: The XML layout file for the main screen, defining the UI elements using `ConstraintLayout` and `MaterialCardView`.
-   **`AndroidManifest.xml`**: Declares all application components (`Activity`, `Service`, `Receiver`) and required permissions.
-   **`res/raw/alarm.mp3`**: The audio file that is played when the alarm goes off (you should have this file in your `res/raw` directory).
