POST http://localhost:8080/api/consultant

```
{
  "firstName": "blaat69",
  "lastName": "meeeeeh",
  "jobTitle": "string",
  "emailAddress": "testy@weplus.be",
  "dateOfBirth": "2024-07-17",
  "skypeAddress": "string",
  "linkedInAccount": "string",
  "twitterAccount": "string",
  "mobile": "string",
  "photo": "string",
  "active": true,
  "type": "COWORKER",
  "mbtiId": "3d08c27b-206f-44f4-90de-5c572e758fbe",
  "location": "string",
  "aboutMeText": "string",
  "workInWorkLocation": [
    "BE"
  ],
  "moveToWorkLocation": [
    "BE"
  ]
}
```

```
type=STANDALONE, roundTripTime=3.4 ms, state=CONNECTED}]
08:20:11.187 [MessageBroker-4] DEBUG org.mongodb.driver.connection - Checkout started for connection to localhost:27017
08:20:11.187 [MessageBroker-4] DEBUG org.mongodb.driver.connection - Connection checked out: address=localhost:27017, driver-generated ID=4, duration=0 ms
08:20:11.187 [MessageBroker-4] DEBUG org.mongodb.driver.protocol.command - Command "aggregate" started on database "cvapp" using a connection with driver-generated ID 4 and server-generated ID 11 to localhost:27017. The request ID is 327 and the operation ID is 326. Command: {"aggregate": "variant", "pipeline": [{"$match": {"status": "ERROR"}}, {"$limit": 1}, {"$group": {"_id": 1, "n": {"$sum": 1}}}], "cursor": {}, "$db": "cvapp", "lsid": {"id": {"$binary": {"base64": "hG0ezb+uSHqRcbyzlhh8dA==", "subType": "04"}}}}
08:20:11.188 [MessageBroker-4] DEBUG org.mongodb.driver.protocol.command - Command "aggregate" succeeded on database "cvapp" in 0.8764 ms using a connection with driver-generated ID 4 and server-generated ID 11 to localhost:27017. The request ID is 327 and the operation ID is 326. Command reply: {"cursor": {"firstBatch": [], "id": 0, "ns": "cvapp.variant"}, "ok": 1.0}
08:20:11.188 [MessageBroker-4] DEBUG org.mongodb.driver.operation - Received batch of 0 documents with cursorId 0 from server localhost:27017
08:20:11.188 [MessageBroker-4] DEBUG org.mongodb.driver.connection - Connection checked in: address=localhost:27017, driver-generated ID=4
08:20:11.510 [MessageBroker-8] DEBUG o.s.d.m.r.query.MongoQueryCreator - Created query Query: { "status" : { "$java" : REQUESTED } }, Fields: {}, Sort: {}
08:20:11.510 [MessageBroker-8] DEBUG o.s.data.mongodb.core.MongoTemplate - Executing count: { "status" : "REQUESTED"} in collection: analysis
08:20:11.511 [MessageBroker-8] DEBUG org.mongodb.driver.cluster - Server selection started for operation with ID 327. Selector: ReadPreferenceServerSelector{readPreference=primary}, topology description: {type=STANDALONE, servers=[{address=localhost:27017, type=STANDALONE, roundTripTime=3.4 ms, state=CONNECTED}]
08:20:11.511 [MessageBroker-8] DEBUG org.mongodb.driver.cluster - Server selection succeeded for operation with ID 327. Selected server: localhost:27017. Selector: ReadPreferenceServerSelector{readPreference=primary}, topology description: {type=STANDALONE, servers=[{address=localhost:27017, type=STANDALONE, roundTripTime=3.4 ms, state=CONNECTED}]
08:20:11.511 [MessageBroker-8] DEBUG org.mongodb.driver.connection - Checkout started for connection to localhost:27017
08:20:11.511 [MessageBroker-8] DEBUG org.mongodb.driver.connection - Connection checked out: address=localhost:27017, driver-generated ID=4, duration=0 ms
08:20:11.511 [MessageBroker-8] DEBUG org.mongodb.driver.protocol.command - Command "aggregate" started on database "cvapp" using a connection with driver-generated ID 4 and server-generated ID 11 to localhost:27017. The request ID is 328 and the operation ID is 327. Command: {"aggregate": "analysis", "pipeline": [{"$match": {"status": "REQUESTED"}}, {"$limit": 1}, {"$group": {"_id": 1, "n": {"$sum": 1}}}], "cursor": {}, "$db": "cvapp", "lsid": {"id": {"$binary": {"base64": "hG0ezb+uSHqRcbyzlhh8dA==", "subType": "04"}}}}
08:20:11.512 [MessageBroker-8] DEBUG org.mongodb.driver.protocol.command - Command "aggregate" succeeded on database "cvapp" in 1.5259 ms using a connection with driver-generated ID 4 and server-generated ID 11 to localhost:27017. The request ID is 328 and the operation ID is 327. Command reply: {"cursor": {"firstBatch": [], "id": 0, "ns": "cvapp.analysis"}, "ok": 1.0}
08:20:11.513 [MessageBroker-8] DEBUG org.mongodb.driver.operation - Received batch of 0 documents with cursorId 0 from server localhost:27017
08:20:11.513 [MessageBroker-8] DEBUG org.mongodb.driver.connection - Connection checked in: address=localhost:27017, driver-generated ID=4
08:20:12.192 [MessageBroker-1] DEBUG o.s.d.m.r.query.MongoQueryCreator - Created query Query: { "status" : { "$java" : REQUESTED } }, Fields: {}, Sort: {}
08:20:12.192 [MessageBroker-1] DEBUG o.s.data.mongodb.core.MongoTemplate - Executing count: { "status" : "REQUESTED"} in collection: variant
08:20:12.192 [MessageBroker-1] DEBUG org.mongodb.driver.cluster - Server selection started for operation with ID 328. Selector: ReadPreferenceServerSelector{readPreference=primary}, topology description: {type=STANDALONE, servers=[{address=localhost:27017, type=STANDALONE, roundTripTime=3.4 ms, state=CONNECTED}]
08:20:12.192 [MessageBroker-1] DEBUG org.mongodb.driver.cluster - Server selection succeeded for operation with ID 328. Selected server: localhost:27017. Selector: ReadPreferenceServerSelector{readPreference=primary}, topology description: {type=STANDALONE, servers=[{address=localhost:27017, type=STANDALONE, roundTripTime=3.4 ms, state=CONNECTED}]
08:20:12.192 [MessageBroker-1] DEBUG org.mongodb.driver.connection - Checkout started for connection to localhost:27017
08:20:12.192 [MessageBroker-1] DEBUG org.mongodb.driver.connection - Connection checked out: address=localhost:27017, driver-generated ID=4, duration=0 ms
08:20:12.193 [MessageBroker-1] DEBUG org.mongodb.driver.protocol.command - Command "aggregate" started on database "cvapp" using a connection with driver-generated ID 4 and server-generated ID 11 to localhost:27017. The request ID is 329 and the operation ID is 328. Command: {"aggregate": "variant", "pipeline": [{"$match": {"status": "REQUESTED"}}, {"$limit": 1}, {"$group": {"_id": 1, "n": {"$sum": 1}}}], "cursor": {}, "$db": "cvapp", "lsid": {"id": {"$binary": {"base64": "hG0ezb+uSHqRcbyzlhh8dA==", "subType": "04"}}}}
08:20:12.194 [MessageBroker-1] DEBUG org.mongodb.driver.protocol.command - Command "aggregate" succeeded on database "cvapp" in 1.3642 ms using a connection with driver-generated ID 4 and server-generated ID 11 to localhost:27017. The request ID is 329 and the operation ID is 328. Command reply: {"cursor": {"firstBatch": [], "id": 0, "ns": "cvapp.variant"}, "ok": 1.0}
08:20:12.194 [MessageBroker-1] DEBUG org.mongodb.driver.operation - Received batch of 0 documents with cursorId 0 from server localhost:27017
08:20:12.194 [MessageBroker-1] DEBUG org.mongodb.driver.connection - Connection checked in: address=localhost:27017, driver-generated ID=4
08:20:12.195 [MessageBroker-1] DEBUG o.s.d.m.r.query.MongoQueryCreator - Created query Query: { "status" : { "$java" : ERROR } }, Fields: {}, Sort: {}
08:20:12.195 [MessageBroker-1] DEBUG o.s.data.mongodb.core.MongoTemplate - Executing count: { "status" : "ERROR"} in collection: variant
08:20:12.195 [MessageBroker-1] DEBUG org.mongodb.driver.cluster - Server selection started for operation with ID 329. Selector: ReadPreferenceServerSelector{readPreference=primary}, topology description: {type=STANDALONE, servers=[{address=localhost:27017, type=STANDALONE, roundTripTime=3.4 ms, state=CONNECTED}]
08:20:12.195 [MessageBroker-1] DEBUG org.mongodb.driver.cluster - Server selection succeeded for operation with ID 329. Selected server: localhost:27017. Selector: ReadPreferenceServerSelector{readPreference=primary}, topology description: {type=STANDALONE, servers=[{address=localhost:27017, type=STANDALONE, roundTripTime=3.4 ms, state=CONNECTED}]
08:20:12.195 [MessageBroker-1] DEBUG org.mongodb.driver.connection - Checkout started for connection to localhost:27017
08:20:12.196 [MessageBroker-1] DEBUG org.mongodb.driver.connection - Connection checked out: address=localhost:27017, driver-generated ID=4, duration=0 ms
08:20:12.196 [MessageBroker-1] DEBUG org.mongodb.driver.protocol.command - Command "aggregate" started on database "cvapp" using a connection with driver-generated ID 4 and server-generated ID 11 to localhost:27017. The request ID is 330 and the operation ID is 329. Command: {"aggregate": "variant", "pipeline": [{"$match": {"status": "ERROR"}}, {"$limit": 1}, {"$group": {"_id": 1, "n": {"$sum": 1}}}], "cursor": {}, "$db": "cvapp", "lsid": {"id": {"$binary": {"base64": "hG0ezb+uSHqRcbyzlhh8dA==", "subType": "04"}}}}
08:20:12.198 [MessageBroker-1] DEBUG org.mongodb.driver.protocol.command - Command "aggregate" succeeded on database "cvapp" in 1.9565 ms using a connection with driver-generated ID 4 and server-generated ID 11 to localhost:27017. The request ID is 330 and the operation ID is 329. Command reply: {"cursor": {"firstBatch": [], "id": 0, "ns": "cvapp.variant"}, "ok": 1.0}
08:20:12.198 [MessageBroker-1] DEBUG org.mongodb.driver.operation - Received batch of 0 documents with cursorId 0 from server localhost:27017
08:20:12.198 [MessageBroker-1] DEBUG org.mongodb.driver.connection - Connection checked in: address=localhost:27017, driver-generated ID=4
08:20:12.517 [MessageBroker-5] DEBUG o.s.d.m.r.query.MongoQueryCreator - Created query Query: { "status" : { "$java" : REQUESTED } }, Fields: {}, Sort: {}
08:20:12.517 [MessageBroker-5] DEBUG o.s.data.mongodb.core.MongoTemplate - Executing count: { "status" : "REQUESTED"} in collection: analysis
08:20:12.517 [MessageBroker-5] DEBUG org.mongodb.driver.cluster - Server selection started for operation with ID 330. Selector: ReadPreferenceServerSelector{readPreference=primary}, topology description: {type=STANDALONE, servers=[{address=localhost:27017, type=STANDALONE, roundTripTime=3.4 ms, state=CONNECTED}]
08:20:12.517 [MessageBroker-5] DEBUG org.mongodb.driver.cluster - Server selection succeeded for operation with ID 330. Selected server: localhost:27017. Selector: ReadPreferenceServerSelector{readPreference=primary}, topology description: {type=STANDALONE, servers=[{address=localhost:27017, type=STANDALONE, roundTripTime=3.4 ms, state=CONNECTED}]
08:20:12.517 [MessageBroker-5] DEBUG org.mongodb.driver.connection - Checkout started for connection to localhost:27017
08:20:12.517 [MessageBroker-5] DEBUG org.mongodb.driver.connection - Connection checked out: address=localhost:27017, driver-generated ID=4, duration=0 ms
08:20:12.517 [MessageBroker-5] DEBUG org.mongodb.driver.protocol.command - Command "aggregate" started on database "cvapp" using a connection with driver-generated ID 4 and server-generated ID 11 to localhost:27017. The request ID is 331 and the operation ID is 330. Command: {"aggregate": "analysis", "pipeline": [{"$match": {"status": "REQUESTED"}}, {"$limit": 1}, {"$group": {"_id": 1, "n": {"$sum": 1}}}], "cursor": {}, "$db": "cvapp", "lsid": {"id": {"$binary": {"base64": "hG0ezb+uSHqRcbyzlhh8dA==", "subType": "04"}}}}
08:20:12.518 [MessageBroker-5] DEBUG org.mongodb.driver.protocol.command - Command "aggregate" succeeded on database "cvapp" in 1.0173 ms using a connection with driver-generated ID 4 and server-generated ID 11 to localhost:27017. The request ID is 331 and the operation ID is 330. Command reply: {"cursor": {"firstBatch": [], "id": 0, "ns": "cvapp.analysis"}, "ok": 1.0}
08:20:12.518 [MessageBroker-5] DEBUG org.mongodb.driver.operation - Received batch of 0 documents with cursorId 0 from server localhost:27017
08:20:12.518 [MessageBroker-5] DEBUG org.mongodb.driver.connection - Connection checked in: address=localhost:27017, driver-generated ID=4
08:20:13.213 [MessageBroker-2] DEBUG o.s.d.m.r.query.MongoQueryCreator - Created query Query: { "status" : { "$java" : REQUESTED } }, Fields: {}, Sort: {}
08:20:13.214 [MessageBroker-2] DEBUG o.s.data.mongodb.core.MongoTemplate - Executing count: { "status" : "REQUESTED"} in collection: variant
08:20:13.214 [MessageBroker-2] DEBUG org.mongodb.driver.cluster - Server selection started for operation with ID 331. Selector: ReadPreferenceServerSelector{readPreference=primary}, topology description: {type=STANDALONE, servers=[{address=localhost:27017, type=STANDALONE, roundTripTime=3.4 ms, state=CONNECTED}]
08:20:13.214 [MessageBroker-2] DEBUG org.mongodb.driver.cluster - Server selection succeeded for operation with ID 331. Selected server: localhost:27017. Selector: ReadPreferenceServerSelector{readPreference=primary}, topology description: {type=STANDALONE, servers=[{address=localhost:27017, type=STANDALONE, roundTripTime=3.4 ms, state=CONNECTED}]
08:20:13.214 [MessageBroker-2] DEBUG org.mongodb.driver.connection - Checkout started for connection to localhost:27017
08:20:13.214 [MessageBroker-2] DEBUG org.mongodb.driver.connection - Connection checked out: address=localhost:27017, driver-generated ID=4, duration=0 ms
08:20:13.214 [MessageBroker-2] DEBUG org.mongodb.driver.protocol.command - Command "aggregate" started on database "cvapp" using a connection with driver-generated ID 4 and server-generated ID 11 to localhost:27017. The request ID is 332 and the operation ID is 331. Command: {"aggregate": "variant", "pipeline": [{"$match": {"status": "REQUESTED"}}, {"$limit": 1}, {"$group": {"_id": 1, "n": {"$sum": 1}}}], "cursor": {}, "$db": "cvapp", "lsid": {"id": {"$binary": {"base64": "hG0ezb+uSHqRcbyzlhh8dA==", "subType": "04"}}}}
08:20:13.215 [MessageBroker-2] DEBUG org.mongodb.driver.protocol.command - Command "aggregate" succeeded on database "cvapp" in 1.0289 ms using a connection with driver-generated ID 4 and server-generated ID 11 to localhost:27017. The request ID is 332 and the operation ID is 331. Command reply: {"cursor": {"firstBatch": [], "id": 0, "ns": "cvapp.variant"}, "ok": 1.0}
08:20:13.215 [MessageBroker-2] DEBUG org.mongodb.driver.operation - Received batch of 0 documents with cursorId 0 from server localhost:27017
08:20:13.215 [MessageBroker-2] DEBUG org.mongodb.driver.connection - Connection checked in: address=localhost:27017, driver-generated ID=4
08:20:13.215 [MessageBroker-2] DEBUG o.s.d.m.r.query.MongoQueryCreator - Created query Query: { "status" : { "$java" : ERROR } }, Fields: {}, Sort: {}
08:20:13.215 [MessageBroker-2] DEBUG o.s.data.mongodb.core.MongoTemplate - Executing count: { "status" : "ERROR"} in collection: variant
08:20:13.215 [MessageBroker-2] DEBUG org.mongodb.driver.cluster - Server selection started for operation with ID 332. Selector: ReadPreferenceServerSelector{readPreference=primary}, topology description: {type=STANDALONE, servers=[{address=localhost:27017, type=STANDALONE, roundTripTime=3.4 ms, state=CONNECTED}]
08:20:13.215 [MessageBroker-2] DEBUG org.mongodb.driver.cluster - Server selection succeeded for operation with ID 332. Selected server: localhost:27017. Selector: ReadPreferenceServerSelector{readPreference=primary}, topology description: {type=STANDALONE, servers=[{address=localhost:27017, type=STANDALONE, roundTripTime=3.4 ms, state=CONNECTED}]
08:20:13.215 [MessageBroker-2] DEBUG org.mongodb.driver.connection - Checkout started for connection to localhost:27017
08:20:13.216 [MessageBroker-2] DEBUG org.mongodb.driver.connection - Connection checked out: address=localhost:27017, driver-generated ID=4, duration=0 ms
08:20:13.216 [MessageBroker-2] DEBUG org.mongodb.driver.protocol.command - Command "aggregate" started on database "cvapp" using a connection with driver-generated ID 4 and server-generated ID 11 to localhost:27017. The request ID is 333 and the operation ID is 332. Command: {"aggregate": "variant", "pipeline": [{"$match": {"status": "ERROR"}}, {"$limit": 1}, {"$group": {"_id": 1, "n": {"$sum": 1}}}], "cursor": {}, "$db": "cvapp", "lsid": {"id": {"$binary": {"base64": "hG0ezb+uSHqRcbyzlhh8dA==", "subType": "04"}}}}
08:20:13.216 [MessageBroker-2] DEBUG org.mongodb.driver.protocol.command - Command "aggregate" succeeded on database "cvapp" in 0.7835 ms using a connection with driver-generated ID 4 and server-generated ID 11 to localhost:27017. The request ID is 333 and the operation ID is 332. Command reply: {"cursor": {"firstBatch": [], "id": 0, "ns": "cvapp.variant"}, "ok": 1.0}
08:20:13.217 [MessageBroker-2] DEBUG org.mongodb.driver.operation - Received batch of 0 documents with cursorId 0 from server localhost:27017
08:20:13.217 [MessageBroker-2] DEBUG org.mongodb.driver.connection - Connection checked in: address=localhost:27017, driver-generated ID=4
08:20:13.522 [MessageBroker-6] DEBUG o.s.d.m.r.query.MongoQueryCreator - Created query Query: { "status" : { "$java" : REQUESTED } }, Fields: {}, Sort: {}
08:20:13.522 [MessageBroker-6] DEBUG o.s.data.mongodb.core.MongoTemplate - Executing count: { "status" : "REQUESTED"} in collection: analysis
08:20:13.522 [MessageBroker-6] DEBUG org.mongodb.driver.cluster - Server selection started for operation with ID 333. Selector: ReadPreferenceServerSelector{readPreference=primary}, topology description: {type=STANDALONE, servers=[{address=localhost:27017, type=STANDALONE, roundTripTime=3.4 ms, state=CONNECTED}]
08:20:13.522 [MessageBroker-6] DEBUG org.mongodb.driver.cluster - Server selection succeeded for operation with ID 333. Selected server: localhost:27017. Selector: ReadPreferenceServerSelector{readPreference=primary}, topology description: {type=STANDALONE, servers=[{address=localhost:27017, type=STANDALONE, roundTripTime=3.4 ms, state=CONNECTED}]
08:20:13.522 [MessageBroker-6] DEBUG org.mongodb.driver.connection - Checkout started for connection to localhost:27017
08:20:13.522 [MessageBroker-6] DEBUG org.mongodb.driver.connection - Connection checked out: address=localhost:27017, driver-generated ID=4, duration=0 ms
08:20:13.523 [MessageBroker-6] DEBUG org.mongodb.driver.protocol.command - Command "aggregate" started on database "cvapp" using a connection with driver-generated ID 4 and server-generated ID 11 to localhost:27017. The request ID is 334 and the operation ID is 333. Command: {"aggregate": "analysis", "pipeline": [{"$match": {"status": "REQUESTED"}}, {"$limit": 1}, {"$group": {"_id": 1, "n": {"$sum": 1}}}], "cursor": {}, "$db": "cvapp", "lsid": {"id": {"$binary": {"base64": "hG0ezb+uSHqRcbyzlhh8dA==", "subType": "04"}}}}
08:20:13.524 [MessageBroker-6] DEBUG org.mongodb.driver.protocol.command - Command "aggregate" succeeded on database "cvapp" in 1.2013 ms using a connection with driver-generated ID 4 and server-generated ID 11 to localhost:27017. The request ID is 334 and the operation ID is 333. Command reply: {"cursor": {"firstBatch": [], "id": 0, "ns": "cvapp.analysis"}, "ok": 1.0}
08:20:13.524 [MessageBroker-6] DEBUG org.mongodb.driver.operation - Received batch of 0 documents with cursorId 0 from server localhost:27017
08:20:13.524 [MessageBroker-6] DEBUG org.mongodb.driver.connection - Connection checked in: address=localhost:27017, driver-generated ID=4
08:20:14.219 [MessageBroker-3] DEBUG o.s.d.m.r.query.MongoQueryCreator - Created query Query: { "status" : { "$java" : REQUESTED } }, Fields: {}, Sort: {}
08:20:14.220 [MessageBroker-3] DEBUG o.s.data.mongodb.core.MongoTemplate - Executing count: { "status" : "REQUESTED"} in collection: variant
08:20:14.221 [MessageBroker-3] DEBUG org.mongodb.driver.cluster - Server selection started for operation with ID 334. Selector: ReadPreferenceServerSelector{readPreference=primary}, topology description: {type=STANDALONE, servers=[{address=localhost:27017, type=STANDALONE, roundTripTime=3.4 ms, state=CONNECTED}]
08:20:14.221 [MessageBroker-3] DEBUG org.mongodb.driver.cluster - Server selection succeeded for operation with ID 334. Selected server: localhost:27017. Selector: ReadPreferenceServerSelector{readPreference=primary}, topology description: {type=STANDALONE, servers=[{address=localhost:27017, type=STANDALONE, roundTripTime=3.4 ms, state=CONNECTED}]
08:20:14.222 [MessageBroker-3] DEBUG org.mongodb.driver.connection - Checkout started for connection to localhost:27017
08:20:14.222 [MessageBroker-3] DEBUG org.mongodb.driver.connection - Connection checked out: address=localhost:27017, driver-generated ID=4, duration=0 ms
08:20:14.222 [MessageBroker-3] DEBUG org.mongodb.driver.protocol.command - Command "aggregate" started on database "cvapp" using a connection with driver-generated ID 4 and server-generated ID 11 to localhost:27017. The request ID is 335 and the operation ID is 334. Command: {"aggregate": "variant", "pipeline": [{"$match": {"status": "REQUESTED"}}, {"$limit": 1}, {"$group": {"_id": 1, "n": {"$sum": 1}}}], "cursor": {}, "$db": "cvapp", "lsid": {"id": {"$binary": {"base64": "hG0ezb+uSHqRcbyzlhh8dA==", "subType": "04"}}}}
08:20:14.224 [MessageBroker-3] DEBUG org.mongodb.driver.protocol.command - Command "aggregate" succeeded on database "cvapp" in 1.6718 ms using a connection with driver-generated ID 4 and server-generated ID 11 to localhost:27017. The request ID is 335 and the operation ID is 334. Command reply: {"cursor": {"firstBatch": [], "id": 0, "ns": "cvapp.variant"}, "ok": 1.0}
08:20:14.224 [MessageBroker-3] DEBUG org.mongodb.driver.operation - Received batch of 0 documents with cursorId 0 from server localhost:27017
08:20:14.224 [MessageBroker-3] DEBUG org.mongodb.driver.connection - Connection checked in: address=localhost:27017, driver-generated ID=4
08:20:14.224 [MessageBroker-3] DEBUG o.s.d.m.r.query.MongoQueryCreator - Created query Query: { "status" : { "$java" : ERROR } }, Fields: {}, Sort: {}
08:20:14.225 [MessageBroker-3] DEBUG o.s.data.mongodb.core.MongoTemplate - Executing count: { "status" : "ERROR"} in collection: variant
08:20:14.225 [MessageBroker-3] DEBUG org.mongodb.driver.cluster - Server selection started for operation with ID 335. Selector: ReadPreferenceServerSelector{readPreference=primary}, topology description: {type=STANDALONE, servers=[{address=localhost:27017, type=STANDALONE, roundTripTime=3.4 ms, state=CONNECTED}]
08:20:14.225 [MessageBroker-3] DEBUG org.mongodb.driver.cluster - Server selection succeeded for operation with ID 335. Selected server: localhost:27017. Selector: ReadPreferenceServerSelector{readPreference=primary}, topology description: {type=STANDALONE, servers=[{address=localhost:27017, type=STANDALONE, roundTripTime=3.4 ms, state=CONNECTED}]
08:20:14.225 [MessageBroker-3] DEBUG org.mongodb.driver.connection - Checkout started for connection to localhost:27017
08:20:14.225 [MessageBroker-3] DEBUG org.mongodb.driver.connection - Connection checked out: address=localhost:27017, driver-generated ID=4, duration=0 ms
08:20:14.225 [MessageBroker-3] DEBUG org.mongodb.driver.protocol.command - Command "aggregate" started on database "cvapp" using a connection with driver-generated ID 4 and server-generated ID 11 to localhost:27017. The request ID is 336 and the operation ID is 335. Command: {"aggregate": "variant", "pipeline": [{"$match": {"status": "ERROR"}}, {"$limit": 1}, {"$group": {"_id": 1, "n": {"$sum": 1}}}], "cursor": {}, "$db": "cvapp", "lsid": {"id": {"$binary": {"base64": "hG0ezb+uSHqRcbyzlhh8dA==", "subType": "04"}}}}
08:20:14.227 [MessageBroker-3] DEBUG org.mongodb.driver.protocol.command - Command "aggregate" succeeded on database "cvapp" in 1.4226 ms using a connection with driver-generated ID 4 and server-generated ID 11 to localhost:27017. The request ID is 336 and the operation ID is 335. Command reply: {"cursor": {"firstBatch": [], "id": 0, "ns": "cvapp.variant"}, "ok": 1.0}
08:20:14.227 [MessageBroker-3] DEBUG org.mongodb.driver.operation - Received batch of 0 documents with cursorId 0 from server localhost:27017
08:20:14.227 [MessageBroker-3] DEBUG org.mongodb.driver.connection - Connection checked in: address=localhost:27017, driver-generated ID=4
08:20:14.530 [MessageBroker-7] DEBUG o.s.d.m.r.query.MongoQueryCreator - Created query Query: { "status" : { "$java" : REQUESTED } }, Fields: {}, Sort: {}
08:20:14.530 [MessageBroker-7] DEBUG o.s.data.mongodb.core.MongoTemplate - Executing count: { "status" : "REQUESTED"} in collection: analysis
08:20:14.530 [MessageBroker-7] DEBUG org.mongodb.driver.cluster - Server selection started for operation with ID 336. Selector: ReadPreferenceServerSelector{readPreference=primary}, topology description: {type=STANDALONE, servers=[{address=localhost:27017, type=STANDALONE, roundTripTime=3.4 ms, state=CONNECTED}]
08:20:14.530 [MessageBroker-7] DEBUG org.mongodb.driver.cluster - Server selection succeeded for operation with ID 336. Selected server: localhost:27017. Selector: ReadPreferenceServerSelector{readPreference=primary}, topology description: {type=STANDALONE, servers=[{address=localhost:27017, type=STANDALONE, roundTripTime=3.4 ms, state=CONNECTED}]
08:20:14.530 [MessageBroker-7] DEBUG org.mongodb.driver.connection - Checkout started for connection to localhost:27017
08:20:14.530 [MessageBroker-7] DEBUG org.mongodb.driver.connection - Connection checked out: address=localhost:27017, driver-generated ID=4, duration=0 ms
08:20:14.530 [MessageBroker-7] DEBUG org.mongodb.driver.protocol.command - Command "aggregate" started on database "cvapp" using a connection with driver-generated ID 4 and server-generated ID 11 to localhost:27017. The request ID is 337 and the operation ID is 336. Command: {"aggregate": "analysis", "pipeline": [{"$match": {"status": "REQUESTED"}}, {"$limit": 1}, {"$group": {"_id": 1, "n": {"$sum": 1}}}], "cursor": {}, "$db": "cvapp", "lsid": {"id": {"$binary": {"base64": "hG0ezb+uSHqRcbyzlhh8dA==", "subType": "04"}}}}
08:20:14.531 [MessageBroker-7] DEBUG org.mongodb.driver.protocol.command - Command "aggregate" succeeded on database "cvapp" in 1.0261 ms using a connection with driver-generated ID 4 and server-generated ID 11 to localhost:27017. The request ID is 337 and the operation ID is 336. Command reply: {"cursor": {"firstBatch": [], "id": 0, "ns": "cvapp.analysis"}, "ok": 1.0}
08:20:14.531 [MessageBroker-7] DEBUG org.mongodb.driver.operation - Received batch of 0 documents with cursorId 0 from server localhost:27017
08:20:14.531 [MessageBroker-7] DEBUG org.mongodb.driver.connection - Connection checked in: address=localhost:27017, driver-generated ID=4

```

## Consultant

Request URL:

http://localhost:8080/api/consultant/88c55879-46b8-4e73-a592-a26e137355fb/resume

Request Method:

GET

Status Code:

500 Internal Server Error

Remote Address:

[::1]:8080

Referrer Policy:

strict-origin-when-cross-origin

```bash
curl -X 'GET' \
  'http://localhost:8080/api/consultant/49fdcda7-623d-409d-be90-5dbdd0b6d2d8/resume' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer xxx'
```



## Training POST / PUT

[/consultant/{id}/training](http://localhost:8080/api/swagger-ui/index.html#/training-controller/editTraining)

```json
{
  "id": "95cbfbca-6946-449a-b9a4-fbbcbc92d467"
}
```

```json
{
  "title": "trololol",
  "organisation": {
    "id": "string",
    "name": "string",
    "country": {
      "code": "NL",
      "name": {
        "nl": "Nederlands",
        "en": "Nederlands",
        "fr": "Nederlands"
      },
      "preferred": true
    }
  },
  "type": "ACADEMIC",
  "yearStarting": 2024,
  "yearEnding": 2025,
  "thesisTitle": "string"
}
```

```json
{
  "title": "trololol",
  "organisation": {
    "id": "string",
    "name": "string",
    "country": {
      "code": "NL",
      "name": {
        "nl": "Nederlands",
        "en": "Nederlands",
        "fr": "Nederlands"
      },
      "preferred": true
    }
  },
  "type": "CERTIFICATE",
  "year": 2024
}
```

```json
[
  {
  "title": "trololol",
  "organisation": {
    "id": "string",
    "name": "string",
    "country": {
      "code": "NL",
      "name": {
        "nl": "Nederlands",
        "en": "Nederlands",
        "fr": "Nederlands"
      },
      "preferred": true
    }
  },
  "type": "ACADEMIC",
  "yearStarting": 2024,
  "yearEnding": 2025,
  "thesisTitle": "string"
  }
]
```

```json
{
  "datetime": "2024-06-24T00:14:31.9823638Z",
  "timestamp": 1719188071,
  "status": 404,
  "error": "app.back-end.error.consultant.not_found",
  "message": "Consultant can not be found",
  "fieldErrors": []
}
```