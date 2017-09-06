#Simple docker service for xhprof

## Setup you xhprof
set output dir to ./log ini php.ini file 
```
[xhprof]
extension=xhprof.so
xhprof.output_dir="/path/to/docker/log"

```
##Build docker Grapfviz

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