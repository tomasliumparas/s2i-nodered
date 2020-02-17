[![Build Status](https://drone.getais.cloud/api/badges/tomasliumparas/s2i-nodered/status.svg)](https://drone.getais.cloud/tomasliumparas/s2i-nodered)

# Node-red S2I container image
This container image includes Node-red for OpenShift and general usage.

Image is built is as follows:
```bash
s2i-nodejs-10-git-centos7 - Original nodejs-10-centos7 builder image updated to include GIT v.2.X so that project feature could be enabled
s2i-nodered-base-centos7 - S2I build from Node-red package.json using s2i-nodejs-10-git
s2i-nodered-centos7 - Enabling S2I over s2i-nodered-base image
```

Note: while the examples in this README are calling podman, you can replace any such calls by docker with the same arguments

## Description
Node-RED is a programming tool for wiring together hardware devices, APIs and online services in new and interesting ways.

It provides a browser-based editor that makes it easy to wire together flows using the wide range of nodes in the palette that can be deployed to its runtime in a single-click.

## Usage
The structure of example-app can look like this:
```
./flows.json
```
A file containing Node-red flows

```
./settings.js
```
An override Node-red settings file


### Building on OpenShift
If you want to create a new container layered image, you can use the Source build feature of Openshift. To create a new Node-red application in Openshift, while using data available in test-app on the host, execute the following command:
```bash
git clone https://github.com/tomasliumparas/s2i-nodered.git
cd s2i-nodered
oc new-app getais/s2i-nodered-centos7:latest~. --context-dir example-app --name nodered-example-app
```

Or without locally cloning the repository:
```bash
oc new-app getais/s2i-nodered-centos7:latest~https://github.com/tomasliumparas/s2i-nodered.git --context-dir example-app --name nodered-example-app
```

Checking if example application is working (from within the OpenShift cluster):
```bash
curl nodered-test-app.<openshift-project>.svc:1880/hello
Hello OpenShift!
```

Creating OpenShift route:
```bash
oc expose 

### Building using standalone S2i
The same application can also be built using the standalone S2I application on systems that have it available
```bash
$ s2i build example-app/ getais/s2i-nodered-centos7 nodered-example-app
```



## Environment variables and volumes
The Apache HTTP Server container image supports the following configuration variables:

```
TBD
```

## Default user
By default, Node-red container runs as UID 1001. That means the volume mounted directories for the files (if mounted using -v option) need to be prepared properly, so the UID 1001 can read them.


