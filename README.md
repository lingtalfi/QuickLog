QuickLog
==============
2015-10-12 -> 2021-03-05




Lightweight object to quickly send a message to a log file.


QuickLog is part of the [universe framework](https://github.com/karayabin/universe-snapshot).


Install
==========
Using the [planet installer](https://github.com/lingtalfi/Light_PlanetInstaller) via [light-cli](https://github.com/lingtalfi/Light_Cli)
```bash
lt install Ling.QuickLog
```

Using the [uni](https://github.com/lingtalfi/universe-naive-importer) command.
```bash
uni import Ling/QuickLog
```


Features
------------

 - Lightweight (less than 250 lines of code)
 - quick setup
 - handles multiple log files in parallel  
 - handles rotation of the log file based on the max size (in bytes)




Basic Example
-----------

The following example show the minimum setup required to use the QuickLog object.<br>
First, we store the configured QuickLog instance in a variable.<br>
Then, we can use it for the rest of the application.
 


```php

<?php


use Ling\QuickLog\QuickLog;

require_once "bigbang.php"; 




// minimum setup
$oLog = QuickLog::inst()->setDir(__DIR__ . '/log'); // we need to set the dir that will contain all log files


// now we can add entries to our log, the default log is quicklog.txt
$oLog->addEntry('Hello, this is my first log message');


// now can write to another log file, simply by specifying the file name as the second argument
$url = 'http://nonsense.com/ssssssss';
$oLog->addEntry('Oops, not found: '.  $url, 'badurls'); // this message will be written to the badurls.txt file
```


Note: see 
[bigbang technique](https://github.com/lingtalfi/TheScientist/blob/master/convention.portableAutoloader.eng.md)
for more details on the bigbang one liner.



Advanced configuration
-----------

The following example shows all the possible properties for configuring the QuickLog instance.
More details are provided


```php

$o = QuickLog::inst()
->onError(function(){
    // send mail to webmaster
    // default is to throw an exception
})
// onRotate: define a callback like this, or an array of callbacks, using logNames as keys, like maxSize below
->onRotate(function($logName, $maxSize, $lastMsg){
    // sendMailToWebMaster("Hey, webmaster! log $logName has been rotated (max size of $maxSize bytes was exceeded)")
})
->setDir('/path/do/log.dir') // default is the temp dir of the system
->setDefaultName('mylog')  // default is quicklog
->setExtension('txt')  // default is txt, or you can use an array like maxSize below
->setSep(------- . PHP_EOL)  // sep is appended after each entry, default is PHP_EOL, or you can use an array, like maxSize below
->setMaxSize(1000000) // in bytes (default=1Mo), the string (int) version
->setMaxSize([
    fileName => 1000000,                // this is the array version of configuring the QuickLog instance
    mylog => 5000000,                   // The array version allows us to configure properties per logName.
]) // in bytes (default=1Mo)

```





Related
------------

- [ApplicationLog class](https://github.com/lingtalfi/ApplicationLog): log for your application
- [InstantLog](https://github.com/lingtalfi/InstantLog): log for instant debug







Dependencies
------------------

- [lingtalfi/Bat 1.04](https://github.com/lingtalfi/Bat)




History Log
===============

- 1.0.4 -- 2021-05-31

    - Removing trailing plus in lpi-deps file (to work with Light_PlanetInstaller:2.0.0 api

- 1.0.3 -- 2021-03-05

    - update README.md, add install alternative

- 1.0.2 -- 2020-12-08

    - Fix lpi-deps not using natsort.

- 1.0.1 -- 2020-12-04

    - Add lpi-deps.byml file

- 1.0.0 -- 2015-10-12

    - initial commit

