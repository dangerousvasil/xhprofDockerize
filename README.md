## Setup you xhprof
set output dir to ./log ini php.ini file 
```
[xhprof]
extension=xhprof.so
xhprof.output_dir="/path/to/docker/log"

```

## Setup Application 

```
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
## Setup FireBug
```
require_once('/path/to/firephp/FirePHP.class.php');
// Init firephp
$firephp = FirePHP::getInstance(true);

// $run_id gets from setup earlier
$link = "http://127.0.0.1:8080/index.php?run={$run_id}&source=xhprof_dockerize" . PHP_EOL;
$firephp->info($link, 'profiling data');
```

## Build docker Grapfviz

```
docker build -t graphviz .
```

## Run docker service

```
docker-compose up
```

## Enjoy service

```
http://127.0.0.1:8080/
```
