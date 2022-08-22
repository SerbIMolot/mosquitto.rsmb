RSMB: Really Small Message Broker
=================================

The Really Small Message Broker is a server implementation of the MQTT and MQTT-SN protocols. Any client that implements this protocol properly can use this server for sending and receiving messages.

The main reason for using RSMB over the main [Mosquitto](http://mosquitto.org/) codebase is that Mosquitto doesn't currently have support for the MQTT-SN protocol.


## Project History
Modified RSMB broker, that is able to differentiate clients by Client ID, which is sent in responce to CONNECT, with CONNACK or WILLTOPICREQ. 
To use modified MQTT-SN protocol client need to receive Client ID(unsigned short) from broker and append at the end these 2 bytes to all packets that will be send to broker. 

You can read more about the background of RSMB on the Eclipse project page for Mosquitto:
https://www.eclipse.org/proposals/technology.mosquitto/


## Spec Deviations
There are a couple of deviations from official MQTT-SN v1.2 spec.

The gateway now sends client index at the end of message with CONNACK or WILLTOPICREQ, while not changing original message lenght.
The client now appends received from broker client index, adding to end of the sent messages. And broker uses this index to identify client.
All other behaviour is implemented as specified.

## Getting started

RSMB has been tested on Linux, Mac OS and Windows. 

To compile on Linux and Mac, it should be as simple as:

```
cd rsmb/src
make
```

For more detailed information, see the rsmb/doc/gettingstarted.htm document.


## Sample Configuration

```
# Uncomment this to show you packets being sent and received
#trace_output protocol

# Normal MQTT listener
listener 1883 INADDR_ANY
ipv6 true

# MQTT-SN listener
listener 1883 INADDR_ANY mqtts
ipv6 true
```

For a more complex example, see Ian Craggs' blog post:
http://modelbasedtesting.co.uk/?p=44


## Links

- Source code repository: <https://github.com/eclipse/mosquitto.rsmb>
- Find existing bugs or submit a new bug: <https://github.com/eclipse/mosquitto.rsmb/issues>
- Mailing-list: <https://dev.eclipse.org/mailman/listinfo/mosquitto-dev>


[![Travis Build Status (master)](https://travis-ci.org/eclipse/mosquitto.rsmb.svg?branch=master)](https://travis-ci.org/eclipse/mosquitto.rsmb)
