SQLite on iOS fails after 500-1000 "uses" (transactions) during the lifecycle of the app. This example expedites the failure, but even if the loop count is changed to 100, the app will fail after typical real world use paterns.

After 500-1000 transaction completions, the system goes deaf and no more SQLite transactions will be processed.

1 -- TO BUILD AND REPRODUCE THIS ISSUE:

Command Line:

    git clone https://github.com/n8sabes/ionic-sqlite-1000-transactions-ios-bug.git
    cd ionic-sqlite-1000-transactions-ios-bug
    ionic platform add ios
    cordova plugin add https://github.com/brodysoft/Cordova-SQLitePlugin.git
    ionic run ios
      — Click Insert Button on iOS Simulator
    cat [your_path]/ionic-sqlite-1000-transactions-ios-bug/platforms/ios/cordova/console.log


    BUG: Inserts only to 509 - 998 rows and then goes deaf an no more closure callbacks return.

2 -- Change loop count to 100 and repeat test by clicking Insert button multiple times. This should simulate real world use of an app lifecycle. Using collections will only increase the number inserts possible until failure.

3 -- Remove the executeSql call so you have an empty transaction -- failure still occurs.

4 -- Replace the test with WebSQL -- failure still occurs.

5 -- See issue filed with brodysoft/Cordova-SQLitePlugin:
https://github.com/brodysoft/Cordova-SQLitePlugin/issues/190


Not sure if there needs to be some cleanup between calls. I’ve tried with both ngCordova and direct plugin calls. While this example code was forked from CharlesMendes, other projects exhibit the same iOS SQLite failure after 500-1000 cycles.

Any input on the cause / fix is appreciated.
