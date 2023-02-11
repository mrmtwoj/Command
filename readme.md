``` bash

ADB
    adb start-server
    adb kill-server
    adb devices
    adb logcat
    adb logcat -d > [path to file]
    adb logcat -d | grep README.rst
    adb logcat -c
    adb logcat packagename:[priority level: V, D, I, W, E, F, S]
    adb bugreport > [path_to_file]
        Will dump the whole device information like dumpstate, dumpsys and logcat output.
    adb pull [device file location] [local file location]
    adb push [local file location] [device file location]
    adb shell screencap -p /sdcard/screenshot.png
    adb shell screenrecord /sdcard/NotAbleToLogin.mp4
        stop = ctrl+c
    adb install com.myAppPackage
    adb -s [device serial] install com.myAppPackage
    adb -r install com.myAppPackage
        Very important command! The parameter -r means re-install the app and keep its data on the device. Executing this command is simulating the app update process from an older to the latest version of your app. Make sure the current live version is installed on the test device and then install the release candidate with the option -r. Check for problems after simulating the update process.
    adb devices | tail -n +2 | cut -sf 1 | xargs -IX adb -s X install -r com.myAppPackage
    adb uninstall com.myAppPackage
    adb devices | tail -n +2 | cut -sf 1 | xargs -IX adb -s X uninstall com.myAppPackage
    adb shell am start -a android.intent.action.VIEW
    adb shell am start -a android.intent.action.VIEW http://www.stackoverflow.com
    adb shell am start -t image/* -a android.intent.action.VIEW
    adb backup -all -f /tmp/backup.ab
    adb restore /tmp/backup.ab
    adb reboot-bootloader
    adb reboot recovery
    https://developer.android.com/studio/command-line/adb#shellcommands

BusyBox
    adb shell svc wifi enable
    adb shell ip link show wlan0 | busybox awk '/ether/ {print $2}'
    adb shell svc wifi disable
    
Standard Android Tools
    pm list permission-groups
    pm list permissions -g group
    pm list features
    pm list libraries
        all supported libraries
    pm list packages -3
    pm list packages -s
    pm clear [package name]
    pm set-install-location [0 1 2]
    pm path [package name]
    pm grant [package_name] [permission]
    pm revoke [package_name] [permission]
    pm trim-caches desired_free_space
    pm remove-user [user-id]

Drozer
    Starting a session
        adb forward tcp:31415 tcp:31415
        drozer console connect
        drozer console connect --server <ip>
    List modules
        ls
        ls activity
    Retrieving package information
        run app.package.list -f <app name>
        run app.package.info -a <package name>
    Identifying the attack surface
        run app.package.attacksurface <package name>
    Exploiting Activities
        run app.activity.info -a <package name> -u
        run app.activity.start --component <package name> <component name>
        run app.activity.start --component <package name> <component name> --extra <type> <key> <value>
    Exploiting Content Provider
        run app.provider.info -a <package name>
        run scanner.provider.finduris -a <package name>
        run app.provider.query <uri>
        run app.provider.update <uri> --selection <conditions> <selection arg> <column> <data>
        run scanner.provider.sqltables -a <package name>
        run scanner.provider.injection -a <package name>
        run scanner.provider.traversal -a <package name>
    Exploiting Broadcast Receivers
        run app.broadcast.info -a <package name>
        run app.broadcast.send --component <package name> <component name> --extra <type> <key> <value>
        run app.broadcast.sniff --action <action>
    Exploiting Service
        run app.service.info -a <package name>
        run app.service.start --action <action> --component <package name> <component name>
        run app.service.send <package name> <component name> --msg <what> <arg1> <arg2> --extra <type> <key> <value> --bundle-as-obj

```
