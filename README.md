# SecureHealthDataAPI

A secure health plan API with the following functionalities:
Rest API that can handle any structured data in Json - Specifies URIs, status codes, headers, data model, version
Rest API with support for crd operations - Post, Get, Delete
Rest API with support for validation - Json Schema describes the data model for the use case
Controller validates incoming payloads against json schema
The semantics with ReST API operations such as update if not changed/read if changed
Storage of data in key/value store - Implements use case provided
Rest API that can handle any structured data in Json
Rest API with support for crud operations, including merge support, cascaded delete
Rest API with support for validation
Advanced semantics with rest API operations such as update if not changed
Storage of data in key/value store
Search with join using Elastic
Parent-Child indexing
(Patch changes are shown from the Search API)
Queueing
Security


Steps to be followed to demonstrate the above functionality:
 
Used signing key HS512 —> which does not require the username and password as it is token based authentication

Run the below code in terminal for macbook
export JAVA_HOME=/Library/Java/JavaVirtualMachines/microsoft-11.jdk/Contents/Home

      1. Install elasticsearch and Kibana
      2. Open 3 terminals :
      3. In the first terminal, open the bin directory in the downloaded elasticsearch folder
      4. then enter ./elasticsearch
      5. Open browser, http://localhost:9200/ and check elastic status
      6. In the second terminal, open the bin directory in the downloaded kibana folder 
      7. then enter ./kibana
      8. Open browser, http://localhost:5601/app/dev_tools#/console
      9. In the third terminal enter : brew services start rabbitmq
      10. rabbitmq-server
      11. Open browser, http://localhost:15672/#/channels
      12. Open the 4th terminal and start the redis server with the command: redis-server
      13. Similarly, in 5th terminal enter command: redis-cli

In Postman 
Step 1: —> GET request:  http://localhost:8080/token. With the GET Api, we get the bearer token to be used in all other API authorization.

Step 2: POST —> plan —> Pass Bearer token + payload provided in the repo —> output and eTag

Step 3: PATCH
Merge Request:

1. In the header, if no “If-Match” —> 412 precondition failed: because if-match is not present —> even though payload is updated
2. With “If-Match” —> and updated payload and same tag generated from first get request —>200 ok —> ETAG IS UPDATED/CHANGED
3. With “If-Match” —> and updated payload and same tag generated from first get request —> 412
4. With “If-Match” —> and updated payload and UPDATED E-tag generated  —>  200 Ok

Step 4: GET by plan

1. In the header, if "If-None-Match" is given after update with the old eTag then JSON object is not found
2. If-None-Match with updated payload and UPDATED eTag —> get request will have updated data

GET —>  I will pass object id in URL + token —> If-None-Match is passed —> NO JSON

GET —>  I will pass object id in URL + token —> If-None-Match is not passed —> 200 OK status

Step 5: DELETE

Normal flow + Bearer token to be passed
