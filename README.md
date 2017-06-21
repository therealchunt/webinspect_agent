# riches
Add WebInspect Agent to your deployed app

Basic setup: deploy container that holds the war's (tomcat or whatever), add the agent and extract it, then modify the startup just as you would from the agent install guide. This was setup so that you put the needed files in a files directory and adding an additional logs directory for the event.gz output from the Agent (basically offloading it from the image to the host so that when you shutdown, you will have them for upload to ssc).

# Setup (or fork this repo)
- Dockerfile
- files (directory)
  - HPE_Security_Fortify_WebInspect_Runtime_Agent_Java_17.3.tar.gz (17.10)
  - riches.war
- wi_agent_logs (directory)

# Build
```
docker build --no-cache --tag <image> .
```

# Run 
```
docker run -it -p <external_port>:<internal_port> -v /path/to/wi/agent/logs:/usr/local/tomcat/WI_Agent/log <image>
```

Known Issues:
- Need to remove contents of <wi_agent_logs> directory once image is shutdown (subsequent starts of the same image cant write to these files on restart) FIXME
