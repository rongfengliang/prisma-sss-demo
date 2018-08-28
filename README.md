# prisma server side subscriptions

use wiremock && docker for test

## notes

* wiremock mock address

```code

http verb:Post
respose: {
    data:
    url:
    token
}

```

## How to Run

* start docker-compose service instances

```code
cd database

docker-compose up -d
```

* deploy prisma graphql service

> current first time you must comment subscriptions && and then use prisma deploy --force

```code
cd database

prisma deploy  && prisma deploy --force

```

## some test

* createUser

```code
mutation {
  
  createUser(data:{
    name:"appdemo",
    age:444,
    version:"v1"
  }){
    id
    name
    age
    version
  }
}
```

* wiremock message

<pre>
mock_1    | 2018-08-28 04:32:50.866 Request received:
mock_1    | 172.22.0.3 - POST /webhook
mock_1    |
mock_1    | User-Agent: [akka-http/10.1.0]
mock_1    | Host: [mock:8080]
mock_1    | Content-Length: [85]
mock_1    | Content-Type: [application/json]
mock_1    | {"data":{"user":{"node":{"id":"cjld7u53j000n0a50ph4mezug","name":"rong","age":444}}}}
mock_1    |
mock_1    |
mock_1    | Matched response definition:
mock_1    | {
mock_1    |   "status" : 200,
mock_1    |   "body" : "{\"data\":{\"user\":{\"node\":{\"id\":\"cjld7u53j000n0a50ph4mezug\",\"name\":\"rong\",\"age\":444}}}}",
mock_1    |   "headers" : {
mock_1    |     "TOKEN" : "",
mock_1    |     "URL" : "/webhook",
mock_1    |     "content-type" : "application/json"
mock_1    |   },
mock_1    |   "transformers" : [ "response-template" ]
mock_1    | }
mock_1    |
mock_1    | Response:
mock_1    | HTTP/1.1 200
mock_1    | TOKEN: []
mock_1    | URL: [/webhook]
mock_1    | content-type: [application/json]
mock_1    |
mock_1    |
</pre>