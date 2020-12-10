## Achieve End-to-End configuration

For convenience two agents are provided along with their datasource, datamodel and Dockerfile.

These two agents are named `orion-ping` and `orion-rping`.

Both agents are port-agnostic and basically send a "ping" message.<br>
It can be used to :
- validate a PIXEL installation
- monitor the platform
- learn how to deploy an agent using already existing assets

### Validate a PIXEL installation

You may consider running these two agents to validate a fresh PIXEL installation :<br>in order ensure that each component is well-configured and that data goes through all layers of the PIXEL architecture.

The `orion-ping` agent sends each minute a Fiware entity to Pixel.<br>
Retrieving your ping data in the Information Hub validates the segment Orion <-> IH.

The `orion-rping` (remote ping) agent is a daemon agent triggered outside of PIXEL with a simple curl command.<br>
Retrieving your ping data in the Information Hub validates the whole PIXEL installation, including the components facing the port such as the nging reverse proxy, the Keyrock identity manager and the DAL proxy.

### Monitor the platform

The `orion-ping` agent sends each minute a Fiware entity to Pixel, performing a heartbeat mechanism that allows to check live that everything is running fine, in fact revealing the current platform status.

One can also graph Ping entities with Kibana to see the past platform status.

### How to deploy your first agent : Getting started

In case you've just written your first agent and wish to deploy it inside the PIXEL architecture, you may consider running these two agents to experiment a first deployment : declaration of the datamodel and datasource, dockerization and managing the DAL Orchestrator.

### Resources

[orion-ping](https://gitpixel.satrdlab.upv.es/orange/orion-ping)

[orion-rping](https://gitpixel.satrdlab.upv.es/orange/orion-rping)

[the Ping datamodel](https://gitpixel.satrdlab.upv.es/iglaub/Data_Models)

Below a sample ping datamodel :

```json
{
  "id": "Ping-2020-11-17T13:44:33.598392Z",
  "type": "Ping",
  "from": {
    "type": "Text",
    "value": "8f11eac9f071-172.17.0.2",
    "metadata": {}
  },
  "source": {
    "type": "Text",
    "value": "urn:pixel:DataSource:Ping",
    "metadata": {}
  }
}
```
