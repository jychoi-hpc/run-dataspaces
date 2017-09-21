Wrapper for DataSpaces server command
=====================================

This is a wrapper command for running dataspaces_server with multiple
applications.

The general form of this comand is as follows:
```
$ run-staging.py SERVER_COMMAND [ : APPLICATION_COMMAND ] *
```

More details of options will be printed with `-h` option:
```
$ run-staging.py -h
```

Example
-------

1. Simple case (1 dataspaces_server/1 stage writer/1 stage reader)

```
$ ./run-staging.py -s 1 --oe server.log : \
        -n 1 --oe reader.log adios_icee -c -r DATASPACES : \
        -v -n 1 --oe writer.log adios_icee -w DATASPACES  
```
