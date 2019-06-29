# WebInspect Agent deployed with app
Add WebInspect Agent to your deployed app

Basic setup: deploy container that holds the war's (tomcat or whatever), add the agent and extract it, then modify the startup just as you would from the agent install guide. The logs directory has the event.tar.gz output from the Agent (basically offloading it from the container to the host so that when you shutdown, you will have them for upload to ssc).

# Setup
- Dockerfile
- files (directory)
  - Fortify_WebInspect_Runtime_Agent_Java_<version>.tar.gz
  - app.war

# Create volume for logs
```
docker volume create wi-agent-logs
```
 
# Build
```
docker build --no-cache --tag <image> .
```

# Run 
```
docker run -it -p <external_port>:<internal_port> --mount type=volume,src=wi-agent-logs,dst=/usr/local/tomcat/WI_Agent/log <image>
```
