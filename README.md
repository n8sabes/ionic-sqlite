SQLite on iOS fails after 500-1000 "uses" (transactions) during the lifecycle of the app. This example expedites the failure, but even if the loop count is changed to 100, the app will fail after typical real world use patterns.

SQLite typically goes deaf after 506 cycles.

WebSQL typically goes deaf after 1301 cycles

NOTE: Switching apps (or exiting and re-opening) with CMD+SHIFT+H (Home Button) causes WebSQL to complete the oustanding callbacks. SQLite only completes 1-2 callbacks per switch.

1 -- TO BUILD AND REPRODUCE THIS ISSUE:

    git clone https://github.com/n8sabes/ionic-sqlite-1000-transactions-ios-bug.git
    cd ionic-sqlite-1000-transactions-ios-bug
    ionic platform add ios
    cordova plugin add https://github.com/brodysoft/Cordova-SQLitePlugin.git
    ionic run ios
      — Click Insert Button on iOS Simulator
    cat [your_path]/ionic-sqlite-1000-transactions-ios-bug/platforms/ios/cordova/console.log

----> Watch the log file (or console in XCode) to see the callbacks stop and the plugin goes deaf.

2 -- Change loop count to 100 and repeat test by clicking Insert button multiple times. This should simulate real world use of an app lifecycle. Using collections will only increase the number inserts possible until failure.

3 -- Remove the executeSql call so you have an empty transaction -- failure still occurs.

4 -- Replace the test with WebSQL -- failure still occurs.

5 -- Switch between SQLite and WebSQL by chaning the DB open logic in app.js.

6 -- See issue filed with brodysoft/Cordova-SQLitePlugin:
https://github.com/brodysoft/Cordova-SQLitePlugin/issues/190


This example code was forked from CharlesMendes for ease, but other projects exhibit the same iOS SQLite failure after 500-1000 cycles.

Any input on the cause / fix is appreciated.
