# API

## Connecting to API

To connect to API's you can use basic authorization or an authorization token.

To generate the authorization token, run the following command:

```bash
curl -XPUT http://localhost:9200/_logserver/login -H 'Content-type: application/json' -d '
{
  "username": "$USER",
  "password": "$PASSWORD"
}'
```

The result of the command will return the value of the token and you can use it in the API by passing it as a "token" header, for example:

```bash
curl: -H 'token: 192783916598v51j928419b898v1m79821c2'
```

## Dashboards API

The Dashboards import/export APIs allow people to import dashboards along with all of their corresponding saved objects such as visualizations, saved searches, and index patterns.

### Dashboards Import API

Request:

```bash
POST /api/opensearch-dashboards/dashboards/import
```

Query Parameters:

- `force` (optional)

  (boolean) Overwrite any existing objects on id conflict.
  
- `exclude` (optional)

  (array) Saved object types that should not be imported

Example:

```bash
curl -XPOST -ulogserver:<password> -H "osd-xsrf: true" -H "Content-Type: application/json" "https://127.0.0.1:5601/api/opensearch-dashboards/dashboards/import?force=true" -d@"${DASHBOARD-FILE}"
```

### Dashboards Export API

Request:

```bash
GET /api/opensearch-dashboards/dashboards/export
```

Query Parameters

- `dashboard` (required)

  (array|string) The id(s) of the dashboard(s) to export

Example:

```bash
curl -XGET -ulogserver:<password> -H "osd-xsrf: true" -H "Content-Type: application/json" "https://127.0.0.1:5601/api/opensearch-dashboards/dashboards/export?dashboard=${DASHBOARD-ID}" > ${DASHBOARD-FILE} 
```

## Elasticsearch API

The Elasticsearch has a typical REST API and data is received in JSON format after the HTTP protocol.
By default the tcp/9200 port is used to communicate with the Elasticsearch API.
For purposes of examples, communication with the Elasticsearch API will be carried out using the *curl*
application.

Program syntax:

```bash
curl -XGET -u login:password '127.0.0.1:9200'
```

Available methods:

- PUT - sends data to the server;
- POST - sends a request to the server for a change;
- DELETE - deletes the index / document;
- GET - gets information about the index /document;
- HEAD - is used to check if the index / document exists.

Avilable APIs by roles:

- Index API - manages indexes;
- Document API - manges documnets;
- Cluster API - manage the cluster;
- Search API - is userd to search for data.

## Elasticsearch Index API ##

The indices APIs are used to manage individual indices,
index settings, aliases, mappings, and index templates.

### Adding Index ###

***Adding Index*** - autormatic method:

```bash
curl -XPUT -u login:password '127.0.0.1:9200/twitter/tweet/1?pretty=true' -d'{
    "user" : "elk01",
    "post_date" : "2017-09-05T10:00:00",
    "message" : "tests auto index generation"
    }'
```

You should see the output:

```bash
{
"_index" : "twitter",
  "_type" : "tweet",
  "_id" : "1",
  "_version" : 1,
  "_shards" : {
    "total" : 2,
    "successful" : 1,
    "failed" : 0
  },
  "created" : true
}
```

The parameter `action.auto_create_index` must be set on `true`.

***Adding Index*** – manual method:

- settings the number of shards and replicas:

```bash
curl -XPUT -u login:password '127.0.0.1:9200/twitter2?pretty=true' -d'{
	"settings" : {
	"number_of_shards" : 1,
    "number_of_replicas" : 1
    }
 }'
```

You should see the output:

```bash
{
  "acknowledged" : true
}
```

- command for manual index generation:


```bash
curl -XPUT -u login:password '127.0.0.1:9200/twitter2/tweet/1?pretty=true' -d'{
                "user" : "elk01",
                "post_date" : "2017-09-05T10:00:00",
                "message" : "tests manual index generation"
            }'
```

You should see the output:

```bash
{
  "_index" : "twitter2",
  "_type" : "tweet",
  "_id" : "1",
  "_version" : 1,
  "_shards" : {
    "total" : 2,
     "successful" : 1,
     "failed" : 0
  },
  "created" : true
}
```

### Delete Index  ###


***Delete Index***  - to delete *twitter* index you need use the following command:

```bash
curl -XDELETE -u login:password '127.0.0.1:9200/twitter?pretty=true'
```

The delete index API can also be applied to more than one index, by either using 
a comma separated list, or on all indice by using _all or * as index:

```bash
curl -XDELETE -u login:password '127.0.0.1:9200/twitter*?pretty=true'
```

To allowing to delete indices via wildcards set `action.destructive_requires_name`
setting in the config to `false`.

### API useful commands ###

- get information about Replicas and Shards:

```bash
curl -XGET -u login:password '127.0.0.1:9200/twitter/_settings?pretty=true'
```

```bash
curl -XGET -u login:password '127.0.0.1:9200/twitter2/_settings?pretty=true'
```

- get information about mapping and alias in the index:

```bash
curl -XGET -u login:password '127.0.0.1:9200/twitter/_mappings?pretty=true'
```

```bash
curl -XGET -u login:password '127.0.0.1:9200/twitter/_aliases?pretty=true'
```

- get all information about the index:

```bash
curl -XGET -u login:password '127.0.0.1:9200/twitter?pretty=true'
```

- checking does the index exist:

```bash
curl -XGET -u login:password '127.0.0.1:9200/twitter?pretty=true'
```

- close the index:

```bash
curl -XPOST -u login:password '127.0.0.1:9200/twitter/_close?pretty=true'
```

- open the index:

```bash
curl -XPOST -u login:password '127.0.0.1:9200/twitter/_open?pretty=true'
```

- get the status of all indexes:

```bash
curl -XGET -u login:password '127.0.0.1:9200/_cat/indices?v'
```

- get the status of one specific index:

```bash
curl -XGET -u login:password '127.0.0.1:9200/_cat/indices/twitter?v'
```

- display how much memory is used by the indexes:

```bash
curl -XGET -u login:password '127.0.0.1:9200/_cat/indices?v&h=i,tm&s=tm:desc'
```

- display details of the shards:

```bash
curl -XGET -u login:password '127.0.0.1:9200/_cat/shards?v'
```

## Elasticsearch Document API ##

### Create Document ###

- create a document with a specify ID:

```bash
curl -XPUT -u login:password '127.0.0.1:9200/twitter/tweet/1?pretty=true' -d'{
    "user" : "lab1",
    "post_date" : "2017-08-25T10:00:00",
    "message" : "testuje Elasticsearch"
}'
```

You should see the output:

```bash
{
  "_index" : "twitter",
  "_type" : "tweet",
  "_id" : "1",
  "_version" : 1,
  "_shards" : {
    "total" : 2,
    "successful" : 1,
    "failed" : 0
  },
  "created" : true
}
```

- creating a document with an automatically generated ID: (note: PUT-> POST):

```bash
curl -XPOST -u login:password '127.0.0.1:9200/twitter/tweet?pretty=true' -d'{
    "user" : "lab1",
    "post_date" : "2017-08-25T10:10:00",
    "message" : "testuje automatyczne generowanie ID"
    }'
```

   


You should see the output:

```bash
{
  "_index" : "twitter",
  "_type" : "tweet",
  "_id" : "AV49sTlM8NzerkV9qJfh",
  "_version" : 1,
  "_shards" : {
    "total" : 2,
    "successful" : 1,
    "failed" : 0
  },
  "created" : true
}
```

### Delete Document ###

- delete a document by ID:

```bash
curl -XDELETE -u login:password '127.0.0.1:9200/twitter/tweet/1?pretty=true'
```

```bash
curl -XDELETE -u login:password '127.0.0.1:9200/twitter/tweet/AV49sTlM8NzerkV9qJfh?pretty=true'
```

- delete a document using a wildcard:

```bash
curl -XDELETE -u login:password '127.0.0.1:9200/twitter/tweet/1*?pretty=true'
```

   (parametr:  action.destructive_requires_name must be set to false)

### Useful commands ###

- get information about the document:

```bash
curl -XGET -u login:password '127.0.0.1:9200/twitter/tweet/1?pretty=true'
```

   You should see the output:

```bash
{
    "_index" : "twitter",
    "_type" : "tweet",
    "_id" : "1",
    "_version" : 1,
    "found" : true,
    "_source" : {
        "user" : "lab1",
        "post_date" : "2017-08-25T10:00:00",
        "message" : "testuje Elasticsearch"
    }
}
```

   

- get the source of the document:

```bash
curl -XGET -u login:password '127.0.0.1:9200/twitter/tweet/1/_source?pretty=true'
```

   You should see the output:

```bash
{
    "user" : "lab1",
    "post_date" : "2017-08-25T10:00:00",
    "message" : "test of Elasticsearch"
}
```

   

- get information about all documents in the index:

```bash
curl -XGET -u login:password '127.0.0.1:9200/twitter*/_search?q=*&pretty=true'
```

   You should see the output:

```bash
{
    "took" : 7,
    "timed_out" : false,
    "_shards" : {
        "total" : 10,
        "successful" : 10,
        "failed" : 0
},
"hits" : {
    "total" : 3,
    "max_score" : 1.0,
    "hits" : [ {
        "_index" : "twitter",
        "_type" : "tweet",
        "_id" : "AV49sTlM8NzerkV9qJfh",
        "_score" : 1.0,
        "_source" : {
        "user" : "lab1",
        "post_date" : "2017-08-25T10:10:00",
            "message" : "auto generated ID"
            }
        }, {
         "_index" : "twitter",
         "_type" : "tweet",
         "_id" : "1",
         "_score" : 1.0,
         "_source" : {
           "user" : "lab1",
           "post_date" : "2017-08-25T10:00:00",
           "message" : "Elasticsearch test"
         }
       }, {
         "_index" : "twitter2",
         "_type" : "tweet",
         "_id" : "1",
         "_score" : 1.0,
         "_source" : {
           "user" : "elk01",
           "post_date" : "2017-09-05T10:00:00",
           "message" : "manual index created test"
         }
       } ]
     }
   }
```

   

- the sum of all documents in a specified index:

   ```bash
       curl -XGET -u login:password '127.0.0.1:9200/_cat/count/twitter?v'
   ```

You should see the output:

   ```bash
   epoch              timestamp count
   1504281400     17:56:40     2
   ```

- the sum of all document in Elasticsearch database:

   ```bash
   curl -XGET -u login:password '127.0.0.1:9200/_cat/count?v'
   ```

You should see the output:

```bash
epoch              timestamp count
    1504281518     17:58:38    493658
```

## Elasticsearch Cluster API ##

### Useful commands ###

- information about the cluster state:

bash```
curl -XGET -u login:password '127.0.0.1:9200/_cluster/health?pretty=true'
```

- information about the role and load of nodes in the cluster:

​```bash
curl -XGET -u login:password '127.0.0.1:9200/_cat/nodes?v'
```

- information about the available and used place on the cluster nodes:
```bash
curl -XGET -u login:password '127.0.0.1:9200/_cat/allocation?v'
```

- information which node is currently in the master role:
```bash
curl -XGET -u login:password '127.0.0.1:9200/_cat/master?v'
```

- information abut currently performed operations by the cluster:
```bash
curl -XGET -u login:password '127.0.0.1:9200/_cat/pending_tasks?v' 
```

- information on revoceries / transferred indices:
```bash
curl -XGET -u login:password '127.0.0.1:9200/_cat/recovery?v'
```

- information about shards in a cluster:

```bash
curl -XGET -u login:password '127.0.0.1:9200/_cat/shards?v'
```

- detailed inforamtion about the cluster:

```bash
curl -XGET -u login:password '127.0.0.1:9200/_cluster/stats?human&pretty'
```

- detailed information about the nodes:

```bash
curl -XGET -u login:password '127.0.0.1:9200/_nodes/stats?human&pretty'
```

## Elasticsearch Search API ##

### Useful commands ###

- searching for documents by the string:


```bash
curl -XPOST -u login:password '127.0.0.1:9200/twitter*/tweet/_search?pretty=true' -d '{
        "query": {
            "bool" : {
                "must" : {
                    "query_string" : {
                        "query" : "test"
                    }
                }
            }        
        }
    }'
```

- searching for document by the string and filtering:

```bash
curl -XPOST -u login:password '127.0.0.1:9200/twitter*/tweet/_search?pretty=true' -d'{
   
                "query": {
                        "bool" : {
                                "must" : {
                                    "query_string" : {
                                            "query" : "testuje"
                                        }
                                    },
                                "filter" : {
                                    "term" : { "user" : "lab1" }
                                }
                         }
                 }
        }'
```

- simple search in a specific field (in this case user) uri query:

```bash
curl -XGET -u login:password '127.0.0.1:9200/twitter*/_search?q=user:lab1&pretty=true'
```

- simple search in a specific field:

```bash
curl -XPOST -u login:password '127.0.0.1:9200/twitter*/_search?                pretty=true' -d '{
        "query" : {
        "term" : { "user" : "lab1" }
    }
}'
```


## Elasticsearch - Mapping, Fielddata and Templates ##

Mapping is a collection of fields along with a specific data type
Fielddata is the field in which the data is stored (requires a specific type - string, float)
Template is a template based on which fielddata will be created in a given index.

### Useful commands ###

- Information on all set mappings:

```bash
curl -XGET -u login:password '127.0.0.1:9200/_mapping?pretty=true'
```

- Information about all mappings set in the index:

```bash
curl -XGET -u login:password '127.0.0.1:9200/twitter/_mapping/*?pretty=true'
```

- Information about the type of a specific field:

```bash
curl -XGET -u login:password '127.0.0.1:9200/twitter/_mapping/field/message*?pretty=true'
```

- Information on all set templates:

```bash
curl  -XGET -u login:password '127.0.0.1:9200/_template/*?pretty=true'
```

### Create - Mapping / Fielddata

- Create - Mapping / Fielddata - It creates index twitter-float and the tweet message field sets to float:

```bash
curl -XPUT -u login:password '127.0.0.1:9200/twitter-float?pretty=true' -d '{
       "mappings": {
         "tweet": {
           "properties": {
             "message": {
               "type": "float"
             }
           }
         }
       }
}'

curl -XGET -u login:password '127.0.0.1:9200/twitter-float/_mapping/field/message?pretty=true'
```

### Create Template ###

- Create Template:

```bash
curl -XPUT -u login:password '127.0.0.1:9200/_template/template_1' -d'{
        "template" : "twitter4",
        "order" : 0,
        "settings" : {
            "number_of_shards" : 2
        }
    }'
```

```bash
curl -XPOST -u login:password '127.0.0.1:9200/twitter4/tweet?pretty=true' -d'{
    "user" : "lab1",
    "post_date" : "2017-08-25T10:10:00",
    "message" : "test of ID generation"
}'
```

```bash
curl -XGET -u login:password '127.0.0.1:9200/twitter4/_settings?pretty=true'
```
- Create Template2 - Sets the mapping template for all new indexes specifying that the tweet data, in the 
field called message, should be of the "string" type:

```bash
curl -XPUT -u login:password '127.0.0.1:9200/_template/template_2' -d'{
"template" : "*",
  "mappings": {
        "tweet": {
          "properties": {
            "message": {
              "type": "string"
            }
          }
        }
      }
}'
```

### Delete Mapping ###

- Delete Mapping - Deleting a specific index mapping (no possibility to delete - you need to index):

```bash
curl -XDELETE -u login:password '127.0.0.1:9200/twitter2'
```

### Delete Template ###

- Delete Template:

```bash
curl  -XDELETE -u login:password '127.0.0.1:9200/_template/template_1?pretty=true'
```

## AI Module API ##

### Services ###

The intelligence module has implemented services that allow you to create, modify, delete, execute and read definitions of AI rules.

### List rules ###

The list service returns a list of AI rules definitions stored in the system.

Method: GET
URL:

```bash
https://<host>:<port>/api/ai/list?pretty
```

where:

```bash
host    -    kibana host address
port    -    kibana port
?pretty -    optional json format parameter
```

Curl:

```bash
curl -XGET 'https://localhost:5601/api/ai/list?pretty' -u <user>:<password> -k 
```

Result:
Array of JSON documents:

```bash
| Field                          | Value                                                                               | Screen field (description) |
|--------------------------------|-------------------------------------------------------------------------------------|----------------------------|
| _source.algorithm_type         | GMA, GMAL, LRS, LRST, RFRS, SMAL, SMA, TL                                           | Algorithm.                 |
| _source.model_name             | Not empty string.                                                                   | AI Rule Name.              |
| _source.search                 | Search id.                                                                          | Choose search.             |
| _source.label_field.field      |                                                                                     | Feature to analyse.        |
| _source.max_probes             | Integer value                                                                       | Max probes                 |
| _source.time_frame             | 1 minute, 5 minutes, 15 minutes, 30 minutes, 1 hour, 1 day, 1 week, 30 day, 365 day | Time frame                 |
| _source.value_type             | min, max, avg, count                                                                | Value type                 |
| _source.max_predictions        | Integer value                                                                       | Max predictions            |
| _source.threshold              | Integer value                                                                       | Threshold                  |
| _source.automatic_cron         | Cron format string                                                                  | Automatic cycle            |
| _source.automatic_enable       | true/false                                                                          | Enable                     |
| _source.automatic              | true/false                                                                          | Automatic                  |
| _source.start_date             | YYYY-MM-DD HH:mm or now                                                             | Start date                 |
| _source.multiply_by_values     | Array of string values                                                              | Multiply by values         |
| _source.multiply_by_field      | None or full field name eg.: system.cpu                                             | Multiply by field          |
| _source.selectedroles          | Array of roles name                                                                 | Role                       |
| _source.last_execute_timestamp |                                                                                     | Last execute               |
```

Not screen fields:

| _index                        |   | Elasticsearch index name.           |
|-------------------------------|---|-------------------------------------|
| _type                         |   | Elasticsearch document type.        |
| _id                           |   | Elasticsearch document id.          |
| _source.preparation_date      |   | Document preparation date.          |
| _source.machine_state_uid     |   | AI rule machine state uid.          |
| _source.path_to_logs          |   | Path to ai machine logs.            |
| _source.path_to_machine_state |   | Path to ai machine state files.     |
| _source.searchSourceJSON      |   | Query string.                       |
| _source.processing_time       |   | Process operation time.             |
| _source.last_execute_mili     |   | Last executed time in milliseconds. |
| _source.pid                   |   | Process pid if ai rule is running.  |
| _source.exit_code             |   | Last executed process exit code.    |

### Show rules ###

The show service returns a document of AI rule definition by id.

Method: GET
URL: 
		https://<host>:<port>/api/ai/show/<id>?pretty

where:

	host	-	kibana host address
	port	-	kibana port
	id	-	ai rule document id
	?pretty	-	optional json format parameter

Curl:

```bash
curl -XGET 'https://localhost:5601/api/ai/show/ea9384857de1f493fd84dabb6dfb99ce?pretty' -u <user>:<password> -k
```

Result JSON document:

| Field                          | Value                                                                               | Screen field (description) |
|--------------------------------|-------------------------------------------------------------------------------------|----------------------------|
| _source.algorithm_type         | GMA, GMAL, LRS, LRST, RFRS, SMAL, SMA, TL                                           | Algorithm.                 |
| _source.model_name             | Not empty string.                                                                   | AI Rule Name.              |
| _source.search                 | Search id.                                                                          | Choose search.             |
| _source.label_field.field      |                                                                                     | Feature to analyse.        |
| _source.max_probes             | Integer value                                                                       | Max probes                 |
| _source.time_frame             | 1 minute, 5 minutes, 15 minutes, 30 minutes, 1 hour, 1 day, 1 week, 30 day, 365 day | Time frame                 |
| _source.value_type             | min, max, avg, count                                                                | Value type                 |
| _source.max_predictions        | Integer value                                                                       | Max predictions            |
| _source.threshold              | Integer value                                                                       | Threshold                  |
| _source.automatic_cron         | Cron format string                                                                  | Automatic cycle            |
| _source.automatic_enable       | true/false                                                                          | Enable                     |
| _source.automatic              | true/false                                                                          | Automatic                  |
| _source.start_date             | YYYY-MM-DD HH:mm or now                                                             | Start date                 |
| _source.multiply_by_values     | Array of string values                                                              | Multiply by values         |
| _source.multiply_by_field      | None or full field name eg.: system.cpu                                             | Multiply by field          |
| _source.selectedroles          | Array of roles name                                                                 | Role                       |
| _source.last_execute_timestamp |                                                                                     | Last execute               |

Not screen fields

| _index                        |   | Elasticsearch index name.           |
|-------------------------------|---|-------------------------------------|
| _type                         |   | Elasticsearch document type.        |
| _id                           |   | Elasticsearch document id.          |
| _source.preparation_date      |   | Document preparation date.          |
| _source.machine_state_uid     |   | AI rule machine state uid.          |
| _source.path_to_logs          |   | Path to ai machine logs.            |
| _source.path_to_machine_state |   | Path to ai machine state files.     |
| _source.searchSourceJSON      |   | Query string.                       |
| _source.processing_time       |   | Process operation time.             |
| _source.last_execute_mili     |   | Last executed time in milliseconds. |
| _source.pid                   |   | Process pid if ai rule is running.  |
| _source.exit_code             |   | Last executed process exit code.    |

### Create rules ###

The create service adds a new document with the AI rule definition.

Method: PUT

URL: 

```bash
https://<host>:<port>/api/ai/create
```

where:

	host	-	kibana host address
	port	-	kibana port
	body	-	JSON with definition of ai rule

Curl:

```bash
curl -XPUT 'https://localhost:5601/api/ai/create' -u <user>:<password> -k -H "kbn-version: 6.2.4" -H 'Content-type: application/json' -d' {"algorithm_type":"TL","model_name":"test","search":"search:6c226420-3b26-11e9-a1c0-4175602ff5d0","label_field":{"field":"system.cpu.idle.pct"},"max_probes":100,"time_frame":"1 day","value_type":"avg","max_predictions":10,"threshold":-1,"automatic_cron":"*/5 * * * *","automatic_enable":true,"automatic_flag":true,"start_date":"now","multiply_by_values":[],"multiply_by_field":"none","selectedroles":["test"]}'
```

Validation:

| Field          | Values                                                                              |
|----------------|-------------------------------------------------------------------------------------|
| algorithm_type | GMA, GMAL, LRS, LRST, RFRS, SMAL, SMA, TL                                           |
| value_type     | min, max, avg, count                                                                |
| time_frame     | 1 minute, 5 minutes, 15 minutes, 30 minutes, 1 hour, 1 day, 1 week, 30 day, 365 day |

Body JSON description:

| Field              | Mandatory        | Value                                                                               | Screen field        |
|--------------------|------------------|-------------------------------------------------------------------------------------|---------------------|
| algorithm_type     | Yes              | GMA, GMAL, LRS, LRST, RFRS, SMAL, SMA, TL                                           | Algorithm.          |
| model_name         | Yes              | Not empty string.                                                                   | AI Rule Name.       |
| search             | Yes              | Search id.                                                                          | Choose search.      |
| label_field.field  | Yes              |                                                                                     | Feature to analyse. |
| max_probes         | Yes              | Integer value                                                                       | Max probes          |
| time_frame         | Yes              | 1 minute, 5 minutes, 15 minutes, 30 minutes, 1 hour, 1 day, 1 week, 30 day, 365 day | Time frame          |
| value_type         | Yes              | min, max, avg, count                                                                | Value type          |
| max_predictions    | Yes              | Integer value                                                                       | Max predictions     |
| threshold          | No (default -1)  | Integer value                                                                       | Threshold           |
| automatic_cron     | Yes              | Cron format string                                                                  | Automatic cycle     |
| Automatic_enable   | Yes              | true/false                                                                          | Enable              |
| automatic          | Yes              | true/false                                                                          | Automatic           |
| start_date         | No (default now) | YYYY-MM-DD HH:mm or now                                                             | Start date          |
| multiply_by_values | Yes              | Array of string values                                                              | Multiply by values  |
| multiply_by_field  | Yes              | None or full field name eg.: system.cpu                                             | Multiply by field   |
| selectedroles      | No               | Array of roles name                                                                 | Role                |


Result:

JSON document with fields:

status - true if ok
id     - id of changed document
message- error message

### Update rules ###

The update service changes the document with the AI rule definition.

Method:POST

URL:

```bash
https://<host>:<port>/api/ai/update/<id>
```

where:

	host	-	kibana host address
	port	-	kibana port
	id	-	ai rule document id
	body	-	JSON with definition of ai rule

Curl:

```bash
curl -XPOST 'https://localhost:5601/api/ai/update/ea9384857de1f493fd84dabb6dfb99ce' -u <user>:<password> -k -H "kbn-version: 6.2.4" -H 'Content-type: application/json' -d'
{"algorithm_type":"TL","search":"search:6c226420-3b26-11e9-a1c0-4175602ff5d0","label_field":{"field":"system.cpu.idle.pct"},"max_probes":100,"time_frame":"1 day","value_type":"avg","max_predictions":100,"threshold":-1,"automatic_cron":"*/5 * * * *","automatic_enable":true,"automatic_flag":true,"start_date":"now","multiply_by_values":[],"multiply_by_field":"none","selectedroles":["test"]}
```

Validation:

	| Field          	| Values                                                                              	|
	|----------------	|-------------------------------------------------------------------------------------	|
	| algorithm_type 	| GMA, GMAL, LRS, LRST, RFRS, SMAL, SMA, TL                                           	|
	| value_type     	| min, max, avg, count                                                                	|
	| time_frame     	| 1 minute, 5 minutes, 15 minutes, 30 minutes, 1 hour, 1 day, 1 week, 30 day, 365 day 	|

Body JSON description:

	| Field              	| Mandatory        	| Value                                                                               	| Screen field        	|
	|--------------------	|------------------	|-------------------------------------------------------------------------------------	|---------------------	|
	| algorithm_type     	| Yes              	| GMA, GMAL, LRS, LRST, RFRS, SMAL, SMA, TL                                           	| Algorithm.          	|
	| model_name         	| Yes              	| Not empty string.                                                                   	| AI Rule Name.       	|
	| search             	| Yes              	| Search id.                                                                          	| Choose search.      	|
	| label_field.field  	| Yes              	|                                                                                     	| Feature to analyse. 	|
	| max_probes         	| Yes              	| Integer value                                                                       	| Max probes          	|
	| time_frame         	| Yes              	| 1 minute, 5 minutes, 15 minutes, 30 minutes, 1 hour, 1 day, 1 week, 30 day, 365 day 	| Time frame          	|
	| value_type         	| Yes              	| min, max, avg, count                                                                	| Value type          	|
	| max_predictions    	| Yes              	| Integer value                                                                       	| Max predictions     	|
	| threshold          	| No (default -1)  	| Integer value                                                                       	| Threshold           	|
	| automatic_cron     	| Yes              	| Cron format string                                                                  	| Automatic cycle     	|
	| Automatic_enable   	| Yes              	| true/false                                                                          	| Enable              	|
	| automatic          	| Yes              	| true/false                                                                          	| Automatic           	|
	| start_date         	| No (default now) 	| YYYY-MM-DD HH:mm or now                                                             	| Start date          	|
	| multiply_by_values 	| Yes              	| Array of string values                                                              	| Multiply by values  	|
	| multiply_by_field  	| Yes              	| None or full field name eg.: system.cpu                                             	| Multiply by field   	|
	| selectedroles      	| No               	| Array of roles name                                                                 	| Role                	|

Result:

JSON document with fields:

		status	-	true if ok
		id	-	id of changed document
		message	-	error message

Run:

The run service executes a document of AI rule definition by id.

Method: GET

URL:

```bash
https://<host>:<port>/api/ai/run/<id>
```

where:

		host	-	kibana host address
		port	-	kibana port
		id	-	ai rule document id

Curl:

```bash
	curl -XGET 'https://localhost:5601/api/ai/run/ea9384857de1f493fd84dabb6dfb99ce' -u <user>:<password> -k
```

Result:

JSON document with fields:

		status	-	true if ok
		id	-	id of executed document
		message	-	message

### Delete rules ###

The delete service removes a document of AI rule definition by id.

Method: DELETE

URL:

```bash
https://<host>:<port>/api/ai/delete/<id>
```

where:

		host	-	kibana host address
		port	-	kibana port
		id	-	ai rule document id
Curl:

```bash
curl -XDELETE 'https://localhost:5601/api/ai/delete/ea9384857de1f493fd84dabb6dfb99ce' -u <user>:<password> -k -H "kbn-version: 6.2.4"
```

Result:

JSON document with fields:

	status	-	true if ok
	id	-	id of executed document
	message	-	message

## Alert module API ##

### Create Alert Rule ###

Method: POST

Host:

```bash
https://127.0.0.1:5601
```

URL:

```bash
/api/admin/alertrules
```

Body:

In the body of call, you must pass the JSON object with the full definition of the rule document:

	| Name                  | Description                                                                                                                                                                      |
	|-----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
	| id                    | Document ID in Elasticsearch                                                                                                                                                     |
	| alertrulename         | Rule name (the Name field from the Create Alert tab  the name must be the same as the alert name)                                                                                |
	| alertruleindexpattern | Index pattern (Index pattern field from the Create Alert tab)                                                                                                                    |
	| selectedroles         | Array of roles that have rights to this rule (Roles field from the Create Alert tab)                                                                                             |
	| alertruletype         | Alert rule type (Type field from the Create Alert tab)                                                                                                                           |
	| alertrulemethod       | Type of alert method (Alert method field from the Create Alert tab)                                                                                                              |
	| alertrulemethoddata   | Data for the type of alert (field Email address if alertrulemethod is email  Path to script / command if alertrulemethod is command  and empty value if alertrulemethod is none) |
	| alertrule_any         | Alert script (the Any field from the Create Alert tab)                                                                                                                           |
	| alertruleimportance   | Importance of the rule (Rule importance box from the Create Alert tab)                                                                                                           |
	| alertruleriskkey      | Field for risk calculation (field from the index indicated by alertruleindexpattern according to which the risk will be counted  Risk key field from the Create Alert tab)       |
	| alertruleplaybooks    | Playbook table (document IDs) attached to the alert (Playbooks field from the Create Alert tab)                                                                                  |
	| enable                | Value Y or N depending on whether we enable or disable the rule                                                                                                                  |
	| authenticator         | Constant value index                                                                                                                                                             |


Result OK:

     "Successfully created rule!!" 

or if fault, error message.

Example:

```bash
curl -XPOST 'https://localhost:5601/api/admin/alertrules' -u user:passowrd -k -H "kbn-version: 6.2.4" -H 'Content-type: application/json' -d'
{
	"id":"test_enable_rest",
	"alertrulename":"test enable rest",
	"alertruleindexpattern":"m*",
	"selectedroles":"",
	"alertruletype":"frequency",
	"alertrulemethod":"email",
	"alertrulemethoddata":"ala@local",
	"alertrule_any":"# (Required, frequency specific)\n# Alert when this many documents matching the query occur within a timeframe\nnum_events: 5\n\n# (Required, frequency specific)\n# num_events must occur within this amount of time to trigger an alert\ntimeframe:\n  minutes: 2\n\n# (Required)\n# A list of Elasticsearch filters used for find events\n# These filters are joined with AND and nested in a filtered query\n# For more info: http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/query-dsl.html\nfilter:\n- term:\n    some_field: \"some_value\"\n\n# (Optional, change specific)\n# If true, Alert will poll Elasticsearch using the count api, and not download all of the matching documents. This is useful is you care only about numbers and not the actual data. It should also be used if you expect a large number of query hits, in the order of tens of thousands or more. doc_type must be set to use this.\n#use_count_query:\n\n# (Optional, change specific)\n# Specify the _type of document to search for. This must be present if use_count_query or use_terms_query is set.\n#doc_type:\n\n# (Optional, change specific)\n# If true, Alert will make an aggregation query against Elasticsearch to get counts of documents matching each unique value of query_key. This must be used with query_key and doc_type. This will only return a maximum of terms_size, default 50, unique terms.\n#use_terms_query:\n\n# (Optional, change specific)\n# When used with use_terms_query, this is the maximum number of terms returned per query. Default is 50.\n#terms_size:\n\n# (Optional, change specific)\n# Counts of documents will be stored independently for each value of query_key. Only num_events documents, all with the same value of query_key, will trigger an alert.\n#query_key:\n\n# (Optional, change specific)\n# Will attach all the related events to the event that triggered the frequency alert. For example in an alert triggered with num_events: 3, the 3rd event will trigger the alert on itself and add the other 2 events in a key named related_events that can be accessed in the alerter.\n#attach_related:",
	"alertruleplaybooks":[],
	"alertruleimportance":50,
	"alertruleriskkey":"beat.hostname",
	"enable":"Y",
	"authenticator":"index"
}
'
```

### Save Alert Rules ###

Method: POST

Host:

```bash
https://127.0.0.1:5601
```

URL:

```bash
/api/alerts/alertrule/saverules
```

Example:

```bash
curl -XGET 'https://127.0.0.1:5601/api/alerts/alertrule/saverules' -u $user:$password -k -H 'Content-type: application/json'
```

## Reports module API ##

### Create new task ###

CURL query to create a new csv report:

```bash
curl -k "https://localhost:5601/api/taskmanagement/export" -XPOST -H 'kbn-xsrf: true' -H 'Content-Type: application/json;charset=utf-8' -u USER:PASSWORD -d '{
  "indexpath": "audit",
  "query": "*",
  "fields": [
    "@timestamp",
    "method",
    "operation",
    "request",
    "username"
  ],
  "initiatedUser": "logserver ",
  "fromDate": "2019-09-18T00:00:00",
  "toDate": "2019-09-19T00:00:00",
  "timeCriteriaField": "@timestamp",
  "export_type": "csv",
  "export_format": "csv",
  "role": ""
}'
```

Answer:

```bash
{"taskId":"1568890625355-cbbe16e1-12ac-b53c-158e-e0919338953c"}
```

### Checking the status of the task ###

```bash
curl -k -XGET -u USER:PASSWORD https://localhost:5601/api/taskmanagement/export/1568890625355-cbbe16e1-12ac-b53c-158e-e0919338953
```

Answer:

 - In progress:

```bash
{"taskId":"1568890766279-56667dc8-6bd4-3f42-1773-08722b623ec1","status":"Processing"}
```

 - Done:

```bash
{"taskId":"1568890625355-cbbe16e1-12ac-b53c-158e-e0919338953c","status":"Complete","download":"http://localhost:5601/api/taskmanagement/export/1568890625355-cbbe16e1-12ac-b53c-158e-e0919338953c/download"}
```

 - Error during execution:

```bash
{"taskId":"1568890794564-120f0549-921f-4459-3114-3ea3f6e861b8","status":"Error Occured"}
```

### Downloading results ###

```bash
curl -k -XGET -u USER:PASSWORD https://localhost:5601/api/taskmanagement/export/1568890625355-cbbe16e1-12ac-b53c-158e-e0919338953c/download > /tmp/audit_report.csv
```

## License module API

You can check the status of the license via the API.

Method: GET

Curl: 

```bash
curl -u $USER:$PASSWORD -X GET http://localhost:9200/_logserver/license
```

Result:

```bash
{"status":200,"nodes":"5","indices":"[*]","customerName":"CUSTOMER","issuedOn":"2023-02-17T16:49:50.136294","validity_in_months":"12","documents":"","version":"7.4.2","expiration_date":"2024-02-17T16:49","days_left":"89","siemPlan":"true","networkProbe":"true","noOfNetworkProbes":"5"}
```

### Reload License API

After changing license files in the Elasticsearch install directory `/usr/share/elasticsearch/license/` (for example if the current license was end) , you must load new license using the following command.

Method: POST

Curl:

```bash
curl -u $USER:$PASSWORD -X POST http://localhost:9200/_logserver/license/reload
```

Result:

```bash
{"status":200,"message":"License has been reloaded!","license valid":"YES","customerName":"example - production license","issuedOn":"2020-12-01T13:33:21.816","validity":"2","logserver version":"7.0.5"}
```

## Role Mapping API

After changing Role Mapping files `/etc/elasticsearch/properties.yml` and `/etc/elasticsearch/role-mapping.yml`, you must load new configuration using the following command.

Method: POST

Curl:

```bash
curl -u $USER:$PASSWORD -X POST http://localhost:9200/_logserver/auth/reload
```

## User Module API

To modify user accounts, you can use the User Module API.

You can modify the following account parameters:

- username;
- password;
- assigned roles;
- default role;
- authenticatior;
- email address.

An example of the modification of a user account is as follows:

```bash
curl -u $user:$password localhost:9200/_logserver/accounts -XPUT -H 'Content-type: application/json' -d '
{
  "username": "logserver",
  "password": "new_password",
  "roles": [
    "admin"
  ],
  "defaultrole": "admin",
  "authenticator": "index",
  "email": ""
}'
```
	
## User Password API
	
To modify user pasword, you can use the User Password API.

An example of the modification of a user password is as follows:	

```bash
curl -u $user:$password -XPUT localhost:9200/_logserver/user/password -H 'Content-type: application/json' -d '
{
  "authenticator": "index",
  "username": "$USERNAME",
  "password": "$NEW_PASSWORD",
  "current_password": "$CURRENT_PASSWORD"
}'
```
