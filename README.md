# genschsa/mssql-server-linux

This is the git repo of the custom [genschsa/mssql-server-linux](https://hub.docker.com/r/genschsa/mssql-server-linux/) Docker image.

This image is an extension of the official [microsoft/mssql-server-linux](https://hub.docker.com/r/microsoft/mssql-server-linux/) Docker image

It adds functionality to initialize a fresh instance. When a container is started for the first time, it will execute any files with extensions .sh or .sql that are found in /docker-entrypoint-initdb.d. Files will be executed in alphabetical order. You can easily populate your SQL Server services by mounting scripts into that directory and provide custom images with contributed data.

## Running this image

```
docker run -p 1433:1433 --name mssql -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=Strong(!)Password' -v $PWD/initdb.d:/docker-entrypoint-initdb.d -d genschsa/mssql-server-linux
```

## Additional information:

 * Linux-based mssql-docker [git repo](https://github.com/Microsoft/mssql-docker/tree/master/linux)
 * Running [SQL Server on Linux](https://docs.microsoft.com/en-us/sql/linux/) on top of an Ubuntu 16.04 base image.
 * Note that the version 2017-CU3 currently (as of Feb. 15, 2018) has a bug described here: [https://github.com/Microsoft/mssql-docker/issues/136](https://github.com/Microsoft/mssql-docker/issues/136)
 * Make sure that the .sh files have UNIX-style (LF) line endings. Depending on your platform and Git configuration, Git may change them to Windows-style (CR+LF). In this case, the container won't start, and you may see a non-informative error message like: 
 ```
 standard_init_linux.go:195: exec user process caused "no such file or directory"'.
```
