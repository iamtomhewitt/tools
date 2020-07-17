# Unity

### Debug a Unity app on Android
`adb logcat -s Unity DEBUG`

### Install an apk file over the wifi
* Connect the device via USB and make sure debugging is working;
* `adb tcpip 5555` This makes the device to start listening for connections on port 5555
* Look up the device IP address with `adb shell netcfg` or `adb shell ifconfig`
* You can disconnect the USB now
* Save the following in a script and run
```bash
@echo off
REM Get IP address
set /p device_ip=Device IP Address: 

REM Connect
echo.
echo Connecting to device
adb connect %device_ip%:5555

REM Install
echo.
echo Installing app
adb install -r "<your apk name>".apk

REM Start the app on the device
echo.
echo Restarting app
adb shell monkey -p <com.your.app.entry.point> -c android.intent.category.LAUNCHER 1

REM Disconnect
echo.
echo Disconnecting from device
adb disconnect %device_ip%:5555
```

### Index Looper
Have an index of an array or list that you want to set back to 0 when you reach the end, or set to the last index in the list when you've reached the start?
```csharp
private int index =0;
index = ++index > yourListOrArray.Count - 1 ? 0 : index
```

### Trouble with VSCode and Namespaces
Try the the comments in the answer from [here](https://answers.unity.com/questions/1696517/20193-unityengineui-and-vs-code.html)

### Extract Meshes From a Model
https://www.reddit.com/r/Unity3D/comments/59pywj/extracting_meshes_from_fbx_files/

### Reset the Pivot of a GameObject
https://solvethesystem.wordpress.com/setpivot/
