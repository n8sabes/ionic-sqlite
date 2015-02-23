This appears to be a bug with >1000 sequential transactions on iOS.

Command Line:

    git clone https://github.com/n8sabes/ionic-sqlite-1000-transactions-ios-bug.git
    cd ionic-sqlite-1000-transactions-ios-bug
    ionic platform add ios
    cordova plugin add https://github.com/brodysoft/Cordova-SQLitePlugin.git
    ionic run ios
      — Click Insert Button on iOS Simulator
    cat [your_path]/ionic-sqlite-1000-transactions-ios-bug/platforms/ios/cordova/console.log


    BUG: Inserts only to 509 - 998 rows and then locks up.

OTHER DETAILS:

This only happens on iOS, not browsers.
This also happens with WebSQL.

Not sure if there needs to be some cleanup between calls. I’ve tried with both ngCordova and direct plugin calls. This was forked based on an existing project by CharlesMendes for ease, but other projects out there exhibit the same problem after 1000 cycles on iOS.

Any input on the cause / fix is appreciated.

