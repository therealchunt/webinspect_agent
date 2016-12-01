# riches
uses tomcat:7.0.73-jre8-alpine docker image as the base

runs Riches war with WebInspect Agent

There are files needed (license agreement with HPE Security Fortify required) and small amounts of setup required in order to use the Dockerfile for this image.

VM setup where running docker from:
- Dockerfile
- files (directory)
  - HPE_Security_Fortify_WebInspect_Runtime_Agent_Java_16.8.tar.gz (16.20)
  - riches.war
- wi_agent_logs (directory)



Build Image
```
docker build --tag [image] .
```

Run Image 
```
docker run -it -p [external_port]:8080 -v [path_to_wi_agent_logs]:/usr/local/tomcat/WI_Agent/log [image]
```

Known Issues:
- Need to remove [wi_agent_logs] directory once image is shutdown (subsequent starts of the same image cant write to this directory on restart)
