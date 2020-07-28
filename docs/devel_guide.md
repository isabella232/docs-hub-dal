# Developer's Guide

## Managing Data Format with Information Hub

To allow the Information Hub to automatically import data from Orion, it was decided to publish Data Sources and Data Formats in the Orion database. That information is fulfilled by the DAL Orchestrator using the information contained in the Dockerfile of the NGSI Agents. 

* DataSource format is 
```
{
    "id": "urn of the data source",
    "type": "DataSource",
    "name": {
        "type": "Text",
        "value": "the source name if it is not an urn"
    }
}
```


* DataModel format is
```
{
    "id": "type name as declared in the orion entity",
    "type": "DataModel",
    "schema": {
        "type": "StructuredValue",
        "value": an object containing the json schema
    },
    "schemaUrl": {
        "type": "string",
        "value": "an url to the schema"
    },
    "schemaEncoded": {
        "type": "STRING_URL_ENCODED",
        "value": "a text version URL encoded of the schema if it contains forbidden characters"
    }
}
```

Here schemaUrl is mandatory, schema should be provided for compatibility reasons with previous version, and schemaEncoded has to be present only if the schema contains forbidden chars.

* SourceModelRelation format is
```
{
    "id": "urn of the relation datasource/dataModel",
    "type": "SourceModelRelation",
    "source": {
        "type": "Text",
        "value": "urn/id of the DataSource"
    },
    "model": {
        "type": "Text",
        "value": "Data Model provide by the DataSource"
    }
}
```

## Additional notes
To facilitate development a docker-compose is provided, with a shell script to create the environment test needed to develop and test the DAL Orchestrator.
This environment allows running the complete tests suite delivered with the software.
The start.sh script allows creating a nodejs environment to develop with DAL Orchestrator.  
Refer to the README.md for detailed documentation of the software architecture.


