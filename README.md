Wrapper command for running staging application
===============================================

This is a wrapper command for running multiple applications with Adios staging methods (FlexPath, DATASPACES, DIMES, etc). By default, using DATASPACES is assumed. However, it supports FlexPath and others.

The general form of this comand is as follows:
```
$ run-staging.py SERVER_COMMAND [ : APPLICATION_COMMAND ] *
```

More details of options will be printed with `-h` option:
```
$ run-staging.py -h
```

An Adios staging example is available at https://github.com/jychoi-hpc/test-adios-staging

Example
-------

1. Simple case (1 dataspaces_server/1 stage writer/1 stage reader)

```
$ ./run-staging.py -s 1 --oe server.log : \
        -n 1 --oe reader.log adios_icee -c -r DATASPACES : \
        -v -n 1 --oe writer.log adios_icee -w DATASPACES  
```

2. Running on Titan

Need to use "--mpicmd" option to specify to use "aprun" launcher.

```
./run-staging.py --noserver --mpicmd aprun : \
    -n 4 adios_icee -w FLEXPATH : \
    -n 4 adios_icee -c -r FLEXPATH
```
