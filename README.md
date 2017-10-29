Wrapper command for running staging application
===============================================

This is a wrapper command written in Python for running multiple
applications with Adios staging methods (FlexPath, DATASPACES, DIMES,
etc). By default, using DATASPACES is assumed. However, it supports
FlexPath and others.

The general form of this comand is as follows:
```
$ stagerun SERVER_COMMAND [ : APPLICATION_COMMAND ] *
```

More details of options will be printed with `-h` option:
```
$ stagerun -h
```

An Adios staging example is available at
https://github.com/jychoi-hpc/test-adios-staging

Installation
------------

`stagerun` is a single python file. You can simply download as follows:

```
$ wget https://raw.githubusercontent.com/jychoi-hpc/stagerun/master/stagerun && chmod +x stagerun
```

Or, you can clone this repository.

Example
-------

1. Simple case (1 dataspaces_server/1 stage writer/1 stage reader)

```
$ ./stagerun -s 1 --oe server.log : \
        -n 1 --oe reader.log adios_icee -c -r DATASPACES : \
        -v -n 1 --oe writer.log adios_icee -w DATASPACES  
```

2. Running on Titan

Need to use "--mpicmd" option to specify to use "aprun" launcher.

```
./stagerun --noserver --mpicmd aprun : \
    -n 4 adios_icee -w FLEXPATH : \
    -n 4 adios_icee -c -r FLEXPATH
```
