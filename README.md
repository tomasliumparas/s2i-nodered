[![Build Status](https://drone.getais.cloud/api/badges/tomasliumparas/s2i-nodered/status.svg)](https://drone.getais.cloud/tomasliumparas/s2i-nodered)

# Node-red S2I container image
This container image includes Node-red for OpenShift and general usage. 

Note: while the examples in this README are calling podman, you can replace any such calls by docker with the same arguments

## Description
Node-RED is a programming tool for wiring together hardware devices, APIs and online services in new and interesting ways.

It provides a browser-based editor that makes it easy to wire together flows using the wide range of nodes in the palette that can be deployed to its runtime in a single-click.

## Usage
An example of the data on the host that will be used for the builder image:
```bash
$ ls -la test-app 
-rw-r--r--. 1 root root 3 Feb 17 02:27 flows.json
```

If you want to create a new container layered image, you can use the Source build feature of Openshift. To create a new Node-red application in Openshift, while using data available in test-app on the host, execute the following command:
```bash
oc new-app nodered-centos7:latest~/test-app --name nodered-test-app
```

The same application can also be built using the standalone S2I application on systems that have it available
```bash
$ s2i build test-app/ getais/nodered-centos7 nodered-test-app
```


The structure of test-app can look like this:
```
./flows.json
```
A file containing Node-red flows

```
./settings.js
```
An override Node-red settings file



## Environment variables and volumes
The Apache HTTP Server container image supports the following configuration variables:

```
TBD
```

## Default user
By default, Node-red container runs as UID 1001. That means the volume mounted directories for the files (if mounted using -v option) need to be prepared properly, so the UID 1001 can read them.


