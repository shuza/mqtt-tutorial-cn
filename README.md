# mqtt-tutorial-cn
MQTT Tutorials 
# Run
The easiest way to run [emqx](https://hub.docker.com/r/emqx/emqx) is using docker. If you have not installed docker yet see [docker installation guide](https://docs.docker.com/install/). To run emqx use below command
```
docker run -p 18083:18083 -p 1883:1883 emqx/emqx
```
It will run and open port 1883 for broker and port 18083 for web dashbaord. To verify your web dashboard go to http://localhost:18083

# Client
* [Go](./golang.md)
* Java
* Python
* JavaScript
