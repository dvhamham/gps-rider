# GPS Rider

**GPS Rider** is a powerful Android app and Xposed module that allows you to change your device's location system-wide, without enabling Android's mock location setting. This is ideal for testing, automation, privacy, and bypassing apps that detect or block mock locations.

---

## 📱 Features

- **System-wide fake location**: Change your device's location for all apps, without enabling mock location.
- **Start/Stop/Toggle fake location**: Control the fake location service easily.
- **Set custom location**: Enter latitude and longitude to set any location.
- **Randomize location**: Randomize your location within a specified radius for extra privacy.
- **Set accuracy**: Control the reported GPS accuracy.
- **Get current fake location**: Retrieve the current spoofed coordinates.
- **Favorites**: Save and quickly switch between favorite locations.
- **Material You UI**: Modern, beautiful, and responsive interface using Jetpack Compose.
- **Intent API**: Control the app programmatically from other apps via Intents.
- **No mock location detection**: Uses advanced Xposed hooks and anti-detection techniques to hide all traces of mock location.
- **Multi-process and system service hooks**: Works at the system level for maximum compatibility.
- **Root/Xposed required**: Works with LSPosed/EdXposed.

---

## 🛠️ How It Works

- **Xposed Hooks**: The app uses Xposed to hook into Android's `LocationManager` and `Location` classes, intercepting location requests from all apps and system services.
- **Bypass Mock Detection**: It forcibly sets `isFromMockProvider` to `false` and uses hidden APIs to prevent apps from detecting that the location is fake.
- **No Mock Location Permission Needed**: You do not need to enable "Allow mock locations" in developer settings.
- **System Service Level**: Hooks are applied at both app and system service levels for maximum reliability.
(<a href="screenshot">Screenshot</a>)

---

## 🏁 Requirements

- **Android 8 (API 26) or higher** (Tested up to Android 16) (minSdk = 26, targetSdk = 35)
- **Rooted device**
- **Xposed Framework** (LSPosed or EdXposed recommended)

---

## 🌍 Supported Languages

- **English** (default)
- *(You can add more by creating `values-xx` folders.)*

---

## 🚀 Installation

1. **Install LSPosed/EdXposed** on your device.
2. **Install GPS Rider APK** (see below).
3. **Enable the module in LSPosed/EdXposed Manager**.
4. **Reboot your device**.
5. **Open GPS Rider and set your desired location**.

---

## 🏗️ Building from Source

```sh
git clone https://github.com/dvhamham/gps-rider.git
cd gps-rider
./gradlew :app:assembleDebug
adb install -r app/build/outputs/apk/debug/app-debug.apk
```

---

## 📡 Supported Intent Commands (API via ADB/Broadcast)

You can control all features of the app programmatically or via ADB commands using Intents. Below is a list of all supported commands with descriptions and practical usage examples:

---

### 1. Start Fake Location
**Description:** Activate the fake location service.

```sh
adb shell am broadcast -a com.dvhamham.START_FAKE_LOCATION
```

---

### 2. Stop Fake Location
**Description:** Deactivate the fake location service.

```sh
adb shell am broadcast -a com.dvhamham.STOP_FAKE_LOCATION
```

---

### 3. Toggle Fake Location
**Description:** Toggle the fake location service (start if stopped, stop if started).

```sh
adb shell am broadcast -a com.dvhamham.TOGGLE_FAKE_LOCATION
```

---

### 4. Set Custom Location
**Description:** Set a new fake location using latitude and longitude.

```sh
adb shell am broadcast -a com.dvhamham.SET_CUSTOM_LOCATION --es latitude "35.6895" --es longitude "139.6917"
```

---

### 5. Set Favorite Location
**Description:** Set the fake location based on a saved favorite name.

```sh
adb shell am broadcast -a com.dvhamham.SET_FAVORITE_LOCATION --es favorite_name "Home"
```

---

### 6. Get Service Status
**Description:** Check if the fake location service is active or not.

```sh
adb shell am broadcast -a com.dvhamham.GET_STATUS
```

---

### 7. Get Current Location
**Description:** Retrieve the current coordinates of the fake location.

```sh
adb shell am broadcast -a com.dvhamham.GET_CURRENT_LOCATION
```

---

### 8. Set Accuracy
**Description:** Set the accuracy of the fake location (in meters).

```sh
adb shell am broadcast -a com.dvhamham.SET_ACCURACY --ef accuracy 5.0
```

---

### 9. Set Altitude
**Description:** Set the altitude of the fake location (in meters).

```sh
adb shell am broadcast -a com.dvhamham.SET_ALTITUDE --es altitude "100.0"
```

---

### 10. Set Speed
**Description:** Set the speed for the fake location (in m/s).

```sh
adb shell am broadcast -a com.dvhamham.SET_SPEED --ef speed 10.0
```

---

### 11. Randomize Location
**Description:** Enable location randomization within a specified radius (in meters).

```sh
adb shell am broadcast -a com.dvhamham.RANDOMIZE_LOCATION --es randomize_radius "50.0"
```

---

### 12. Create New Favorite
**Description:** Save a new location to the favorites list.

```sh
adb shell am broadcast -a com.dvhamham.CREATE_FAVORITE --es favorite_name "Work" --es latitude "40.7128" --es longitude "-74.0060"
```

---

### 13. Delete Favorite
**Description:** Delete a location from favorites by name.

```sh
adb shell am broadcast -a com.dvhamham.DELETE_FAVORITE --es favorite_name "Work"
```

---

### 14. Get Favorites List
**Description:** Display all saved favorite locations.

```sh
adb shell am broadcast -a com.dvhamham.GET_FAVORITES
```

---

### 15. Start Timed Location
**Description:** Activate the timed location feature (experimental).

```sh
adb shell am broadcast -a com.dvhamham.START_TIMED_LOCATION
```

---

### 16. Stop Timed Location
**Description:** Deactivate the timed location feature.

```sh
adb shell am broadcast -a com.dvhamham.STOP_TIMED_LOCATION
```

---

### 17. Load Path File
**Description:** Load a path file (GeoJSON or JSON) from storage.

```sh
adb shell am broadcast -a com.dvhamham.LOAD_PATH_FILE --es path_file "/sdcard/Download/path.json"
```

---

### 18. Set Heading
**Description:** Set the movement heading (in degrees).

```sh
adb shell am broadcast -a com.dvhamham.SET_HEADING --ef heading 90.0
```

---

### 19. Set Bearing
**Description:** Set the bearing for the location (in degrees).

```sh
adb shell am broadcast -a com.dvhamham.SET_BEARING --ef bearing 180.0
```

---

### 20. Get Location History
**Description:** Display the history of set locations.

```sh
adb shell am broadcast -a com.dvhamham.GET_LOCATION_HISTORY
```

---

### 21. Clear Location History
**Description:** Delete all locations from the location history.

```sh
adb shell am broadcast -a com.dvhamham.CLEAR_LOCATION_HISTORY
```

---

### ℹ️ Notes:
- The app must be installed and enabled on the device.
- You can change the values (latitude, longitude, favorite_name, etc.) as needed.
- Some commands may require special permissions or settings.
- For more details, check the app source code or contact the developer.

---

> **Note:** All commands can be executed from other Android apps or via ADB. GPS Rider must be installed and enabled as a service.

---

## ⚠️ Disclaimer

> **Use this app responsibly and only for legitimate purposes such as testing and automation. You are fully responsible for any misuse.**

---

## 👨‍💻 Author

> **Name:** Mohammed Hamham  
>
> **Role:** Full Stack Developer
>
> **Location:** Morocco  
>
> **PayPal for support:** [dv.hamham@gmail.com](https://www.paypal.com/paypalme/mohammedhamham)



**If you liked or benefited from this project, you can support me.**



---

## 📋 License

This project is licensed under the MIT License. 


---
