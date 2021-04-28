# Mixing Windows and Linux workloads in Openshift Demo
In this demo, we will create two container apps (crossplat-app) in both a Windows node and a Linux node. We will expose an API endpoint and validate that they can reach each other once both deployed. 


## 1. Deploy crossplat-app-windows app in OpenShift (using CLI)
```
fabdulkh$ oc create -f crossplat-app-windows.yaml 
deployment.apps/crossplat-app-windows created
service/crossplat-app-windows created
route.route.openshift.io/crossplat-app-windows created
```

Validate the route works and the Linux endpoint cannot be reached (should be expected at this point).

## 2. Create crossplat-app-linux app in Openshift (using GUI)

- Developer Mode
- Add > From Container Image 
```
Image name from external registry: https://quay.io/fabdulkh/crossplat-test-linux
Application: Create Application
Application Name: crossplat-app-linux
Name: crossplat-app-linux 

Deployment / Environment Variables: 
Name/Value: ASPNETCORE_URLS / http://*:8080
Name/Value: FetchUrl / http://crossplat-app-windows:8081/?handler=data
```
- Create container image

## 3. Validate the endpoints are reachable from both sides (Linux and Windows)

- Both crossplat-apps from Linux and Windows containers should reach each other's endpoints. 
