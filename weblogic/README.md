# Weblogic 12.2.1.2 Dockerfile

## Prerequisites

You need an Oracle Account and go to https://container-registry.oracle.com where you need to accept the Oracle Standard Terms and Restrictions.
Then you can use your Oracle credentials to log in:

```
docker login container-registry.oracle.com -u YOUR_USERNAME -p YOUR_PASSWORD
```

## Build Image

```
cd dockerfiles/weblogic
docker build -t dmn1k/wls:12.2.1.2-dev .

```

## Start WLS-Container

```
docker run -d -p7001:7001 -e ADMIN_USERNAME=weblogic -e ADMIN_PASSWORD=Weblogic1 dmn1k/wls:12.2.1.2-dev
```