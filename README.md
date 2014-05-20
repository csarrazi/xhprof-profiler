XhProf profiler
===============

[![Latest Stable Version](https://poser.pugx.org/csa/xhprof-profiler/v/stable.png)](https://packagist.org/packages/csa/xhprof-profiler "Latest Stable Version")
[![Latest Unstable Version](https://poser.pugx.org/csa/xhprof-profiler/v/unstable.png)](https://packagist.org/packages/csa/xhprof-profiler "Latest Unstable Version")
[![SensioLabs Insight](https://insight.sensiolabs.com/projects/41343428-0f52-4448-b5ca-8286e9302e82/mini.png)](https://insight.sensiolabs.com/projects/41343428-0f52-4448-b5ca-8286e9302e82 "SensioLabs Insight")
[![Scrutinizer Quality Score](https://scrutinizer-ci.com/g/csarrazi/xhprof-profiler/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/csarrazi/xhprof-profiler/ "Scrutinizer Quality Score")
[![Code Coverage](https://scrutinizer-ci.com/g/csarrazi/xhprof-profiler/badges/coverage.png?b=master)](https://scrutinizer-ci.com/g/csarrazi/xhprof-profiler/ "Code Coverage")
[![Build Status](https://travis-ci.org/csarrazi/xhprof-profiler.png?branch=master)](https://travis-ci.org/csarrazi/xhprof-profiler "Build status")

Installation
------------

    composer require csa/xhprof-profiler:dev-master

Usage
-----

Create any type of PHP web or console application, then use the following in your code:

```php
<?php

require_once __DIR__ . '/vendor/autoload.php';

use XhProf\Profiler;

$profiler = new Profiler();

$profiler->start();

// Your code

// You may either use $profiler->stop() at the end of the code you wish to do something with the trace,
// or let xhprof-profiler manage it, as it registers a shutdown function automatically.
$trace = $profiler->stop();
```

You can easily store a trace using any storage class implementing ```StorageInterface```:

```php
<?php

require_once __DIR__ . '/vendor/autoload.php';

use XhProf\Profiler;
use XhProf\Storage\MemoryStorage;

$profiler = new Profiler();
$profiler->start();
$trace = $profiler->stop();
$storage = new MemoryStorage();
$storage->store($trace);

```

You may also override the profiler's shutdown function:

```php
<?php

require_once __DIR__ . '/vendor/autoload.php';

use XhProf\Storage\FileStorage;
use XhProf\Profiler;
use XhProf\Trace;

$profiler = new Profiler();

$callback = function (Trace $trace) {
    $storage = new FileStorage();
    $storage->store($trace);

    // Do whatever you want with the trace
};

$profiler->setShutdownFunction($callback);
$profiler->start();
```

If you are using the file storage implementation, you may fetch a trace simply by using the fetch method. You may also
fetch the list of available tokens:

```php
<?php

require_once __DIR__ . '/vendor/autoload.php';

use XhProf\Storage\FileStorage;

$storage = new FileStorage();
echo implode(PHP_EOL, $storage->getTokens());
```

Todo
----

* Improve context support (for both Cli or request contexts).

License
-------

This library is under the MIT license. For the full copyright and license
information, please view the LICENSE file that was distributed with this source
code.

[![Bitdeli Badge](https://d2weczhvl823v0.cloudfront.net/csarrazi/xhprof-profiler/trend.png)](https://bitdeli.com/free "Bitdeli Badge")
