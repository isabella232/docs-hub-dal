# User's Guide

## How to install

The full installation process relies on docker-compose.
The process of the installation is split in three different steps:
* Configuration : You must adapt the docker-compose-*.yaml file and feed the different secrets value
* Build : it is the docker-compose build process, a helper script ./build.sh is provided
* Installation : it is the docker-compose up process, a helper script is provided

Different installation flavour is provided:
* full : it will install all the component
* orion : it will install only orion component
* dal : it will install dal-orchestrator and dal-proxy

By default, the full option is selected

Installation of full DAL
```
cd DataAcquisitionLayer
./build.sh 
./install.sh
```

## Configuration
Platform specifics configuration are done using the docker-compose-*.yaml file and with the configuration of the secrets files for each component

### Environment variables

* Orion Database

| Variable | Description |
| --- | --- |
| MONGO_INITDB_ROOT_USERNAME=mongo | The admin user of the mongo database |
| MONGO_INITDB_DATABASE=admin |	The name of the admin database|
|MONGO_INITDB_ROOT_PASSWORD_FILE	| The path to the admin password secret file (usually do not change this value)|
|ORIONDB_PASSWORD_FILE 	|The internal path to the secret file containing the database password (usually do not change this value)|

* Orion

| Variable | Description |
| --- | --- |
| DB_HOST=dal-orion-db |	The database host|
|DB=orion|	The name of the main database|
|DB_USER=orion|	The user to use to connect|
|DB_PASSWORD_FILE|	The internal path to the secret file containing the database password (usually do not change this value)|

* DAL-Proxy

| Variable | Description |
| --- | --- |
|API_LISTEN_PORT=8080|	The port use by the proxy to listen for management API|
|API_LISTEN_IP	| The IP address use by the proxy to listen for management API|
|PROXY_LISTEN_PORT|	The port use to listen for proxy request|
|PROXY_LISTEN_IP|	The IP use to listen for proxy request|
|ORCHESTRATOR_API_URL|	The URL of the DAL -Orchestrator|
|ORCHESTRATOR_TOKEN_FILE|	The secret file containing the token to access DAL-Orchestrator|
|PROXY_API_TOKEN_FILE|	The secret file containing the token to access |DAL-Proxy management API|

* DAL-Orchestrator

| Variable | Description |
| --- | --- |
|SCHEMA_REPOSITORY_URL|	The URL of the public repository of data models schema|
|SCHEMA_REPOSITORY| The container internal folder where the Data Models repository is mounted on (do not change it)|
|NGSIAGENT_NETWORK| The docker network to use to create new NGSI Agent
|NGSIAGENT_KEY=pixel	|The key to identified NGSI Agent image (do not change it)|
|PROXY_API_URL| The URL of the Proxy management API|
|ORCHESTRATOR_LISTEN_PORT|	The port the orchestrator listens to|
|ORCHESTRATOR_LISTEN_IP|	The IP address the orchestrator listens to|
|ORION_API|	The URL of the ORION API|
|ORCHESTRATOR_TOKEN_FILE|	The secret file containing the token to access DAL-Orchestrator|
|PROXY_API_TOKEN_FILE|	The secret file containing the token to access DAL-Proxy management API|


### Secrets

* Orion Database

| Secret | Description |
| --- | --- |
| orion.db.password|	The password for the user orion (random)|
| orion.db.root.password| The password for the admin user (random)|

* Orion

| Secret | Description |
| --- | --- |
| orion.db.password|	The password for the user orion (random)|

* DAL-Proxy

| Secret | Description |
| --- | --- |
| dal.proxy.api.token|The token to secure Proxy API access (random)|
|dal.orchestrator.api.token| The token to secure Orchestrator API access (random)|

* DAL-Orchestrator

| Secret | Description |
| --- | --- |
| dal.proxy.api.token| The token to secure Proxy API access (random)|
dal.orchestrator.api.token|The token to secure Orchestrator API access (random)|

## Component status

How to check the status of each service once has been deployed
How do you verify the service has been correctly deployed?	
* Orion

Executing "docker-compose ps" to check that the service is in "Up" state.

Check the version API : 
```
curl http://<ip>:<port>/version
```

* Mongo - Database


With the command ```docker-compose ps``` you check that the service is in "Up" status, and with the command ```telnet IP 27001``` that the TCP port is listening

* DAL-Proxy

With the command ```docker-compose ps``` you check that the service is in "Up" status.

Use check status API request : 
```
curl http://<ip management>:<port management>/api/status
```

* DAL-Orchestrator

With the command ```docker-compose ps``` you check that the service is in "Up" status.

Use check status API request : 
```
curl http://<ip management>:<port management>/api/status
```

## Issues & Solution
DAL-Proxy and DAL-Orchestrator synchronize them self at start-up. We do not care in which order they start, so you can restart them if you have any issue with them.

For Orion, rely on the official documentation: [https://fiware-orion.readthedocs.io](https://fiware-orion.readthedocs.io/en/master/)


