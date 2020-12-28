## How to collect JFR recording from a process running inside a Docker container on a remote host

where JFR = [Java Flight Recorder](https://docs.oracle.com/javacomponents/jmc-5-4/jfr-runtime-guide/about.htm#JFRUH170). 

### Login into a remote host

```
HOST='myremotehost.company.com' # set your value
```

`$ ssh ${HOST}`

### Find out a target Docker container id

`$ docker ps`
```
CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES
e90b8831a4b8 nginx ...
```

### Store a Docker container id in a variable
```
CONTAINER_ID='e90b8831a4b8'
IMAGE_ID='nginx' ## just an example
```

### Find out a path to jcmd command
Should be _jcmd_ from the same JRE as a running process uses. We assume that just one JRE present inside a container.

`$ docker run --rm --entrypoint sh ${IMAGE_ID} -c "which jcmd"`

#### An example output
```
/usr/bin/jcmd 
```

### Store a jcmd command path in a variable
```
JCMD_PATH='/usr/bin/jcmd'
PROCESS_PID='1' ## container’s primary process (PID 1)
```

### Start JFR recording (duration = 1 minute)
`docker exec ${CONTAINER_ID} ${JCMD_PATH} ${PROCESS_PID} JFR.start duration=1m filename=/recording1m.jfr`

Wait ~ 1 minute...

### Copy the recoding file from inside a running container
`$ docker cp ${CONTAINER_ID}:/recording1m.jfr ./recording1m.jfr`

One can log off the remote host now. 

### Copy the recoding file from the remote host to your local host
On your local host

`$ scp ${HOST}:~/recording1m.jfr . `

The recoding can be opened by using [Oracle JDK Mission Control](https://www.oracle.com/java/technologies/jdk-mission-control.html).