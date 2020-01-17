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