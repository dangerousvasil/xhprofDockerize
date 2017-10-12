## Setup you xhprof
Для установки скачать ветку в соответвии с версией пхп

```
https://github.com/RustJason/xhprof

cd /root/tmp/pear/cache/xhprof-latest/extension
phpize
./configure 
make
make install
```

set output dir to ./log ini php.ini file 

```ini
[xhprof]
extension=xhprof.so
xhprof.output_dir="/path/to/this/project/log"

```

## Setup Application 

```php
require_once 'xhprof_lib.php';
require_once 'xhprof_runs.php';
\xhprof_enable(XHPROF_FLAGS_CPU + XHPROF_FLAGS_MEMORY);

***
You code here...
***

use XHProfRuns_Default;
$xhprof_data = xhprof_disable();
$xhprof_runs = new XHProfRuns_Default();
$run_id = $xhprof_runs->save_run($xhprof_data, "xhprof_dockerize");
```
## Setup FireBug (optional)
```php
require_once('/path/to/firephp/FirePHP.class.php');
// Init firephp
$firephp = FirePHP::getInstance(true);

// $run_id gets from setup earlier
$link = "http://127.0.0.1:8080/index.php?run={$run_id}&source=xhprof_dockerize" . PHP_EOL;
$firephp->info($link, 'profiling data');
```


## Run docker service

```sh
docker-compose up
```

## Enjoy service

```http
http://127.0.0.1:8080/
```


