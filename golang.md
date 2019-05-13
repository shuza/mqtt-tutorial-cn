# Installation
Eclipse provides a MQTT Go client library named [Paho](https://github.com/eclipse/paho.mqtt.golang). To install Paho package, you need to install Go and set your Go workspace first. 
* You can use below command to install 
```
go get github.com/eclipse/paho.mqtt.golang
```
* Import in your code
```
import "github.com/eclipse/paho.mqtt.golang"
```

# Creating Client
First you need to create a client to subscribe and publish to the MQTT broker
```
func createClient(address string, port int, clientId string) mqtt.Client {
	ops := mqtt.NewClientOptions()
	ops.AddBroker(fmt.Sprintf("tcp://%s:%d", address, port))
	ops.SetClientID(clientId)

	client := mqtt.NewClient(ops)
	token := client.Connect()
	for !token.WaitTimeout(3 * time.Second) {
	}
	if err := token.Error(); err != nil {
		panic(err)
	}

	return client
}
```
Here we have set 3 second as timeout. You can change it according to your need.

# Subscribe
Paho client provides a `Subscribe` method which takes 
* **Topic** at which you want to subscribe for message
* **Qos** quality of service
* **method** which will execute when message is received
```
client.Subscribe(topic, qos, func(client mqtt.Client, message mqtt.Message) {
        //  received message from broker
        //  do your task here
		fmt.Printf("Topic  ::  %v\nMessage  ::  %v\n\n", message.Topic(), string(message.Payload()))
	})
```

# Publish
Paho provides a `Publish` method which will publish a message with the specified Qos and content to the specified topic. It also returns a token to track delivery of the message to the broker.
```
token := client.Publish(topic, qos, true, message)
if token.Wait() && token.Error() != nil {
	fmt.Println("Error  :  ", token.Error())
}
```
