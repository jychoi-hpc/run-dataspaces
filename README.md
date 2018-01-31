Wrapper command for running staging application
===============================================

This is a wrapper command written in Python for running multiple
applications and monitoring them. Designed for running Adios staging applications in parallel,
 it is not restricted to use other general cases where one needs to run multiple applications concurrently.

The general form of this comand is as follows:
```
$ stagerun OPTIONS [ : APPLICATION_COMMAND ] *
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
        -n 1 --oe server.log dataspaces_server -s 1 -c 2 : \
        -n 1 --oe reader.log adios_icee -c -r DATASPACES : \
        -v -n 1 --oe writer.log adios_icee -w DATASPACES  
```

2. Running on Titan

Need to use "--mpicmd" option to specify to use "aprun" launcher.

```
./stagerun --mpicmd aprun : \
    -n 4 adios_icee -w FLEXPATH : \
    -n 4 adios_icee -c -r FLEXPATH
```
