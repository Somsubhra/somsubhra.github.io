---
layout: post
title: Introducing Vertex
---

[Vertex](https://github.com/unifiedthings/vertex) is (will be) an implementation of [Web Thing API specification](https://unifiedthings.github.io/mozilla-wot-spec) by [Mozilla IoT](https://iot.mozilla.org). In layman's terms it will be the software package which will run and power the Internet of Things (IoT) edge nodes or devices. The name 'vertex' signifies an edge running on the internet. Many such 'vertex' nodes will run together in a network to form an Edge Computing Network and provide services in a de-centralized fashion on the internet.

The rest of the post will cover how to build, install and run vertex on a node. Please note that vertex is still under active development and the prototype will miss many specifications. We will keep on updating this post as and when we add new features and capabilities.

#### Dependencies

- go

#### Build Instructions

- Clone the source code

```
$ git clone https://github.com/unifiedthings/vertex
```

- Get the go dependencies

```
$ ./deps.sh
```

- Build the vertex executable

```
$ ./build.sh
```

#### Running the Web Thing API Server

```
$ ./vertex server [port]
```

#### Importing Web Thing Devices

- Add a schema file

```
{
  "@context": "http://iot.schema.org",
  "@type": "Toaster",
  "name":"Acme Toaster",
  "description": "A web connected toaster",
  "properties": {
    "on": {
      "type": "boolean",
      "description": "Whether the toaster is currently heating bread",
      "href": "/properties/on"
    },
    "timeRemaining": {
      "type": "number",
      "unit": "seconds",
      "href": "/properties/timeRemaining"
    }
  }
}
```

- Import using the vertex executable

```
$ ./vertex import toaster /path/to/toaster-schema.json
```

#### Using the Web Thing API

- Get a list of all things

```
$ curl localhost:3000/things
 
[
    {
        "description": "A web connected toaster",
        "links": [
            {
                "href": "/things/toaster/properties",
                "mediaType": "application/json",
                "rel": "properties"
            },
            {
                "href": "/things/toaster/actions",
                "mediaType": "application/json",
                "rel": "actions"
            },
            {
                "href": "/things/toaster/events",
                "mediaType": "application/json",
                "rel": "events"
            }
        ],
        "name": "Acme Toaster",
        "properties": {
            "on": {
                "description": "Whether the toaster is currently heating bread",
                "href": "/things/toaster/properties/on",
                "type": "boolean",
                "unit": ""
            },
            "timeRemaining": {
                "description": "",
                "href": "/things/toaster/properties/timeRemaining",
                "type": "number",
                "unit": "seconds"
            }
        },
        "type": "Toaster"
    }
]
```

- Get details for a particular thing

```
$ curl localhost:3000/things/toaster

{
    "description": "A web connected toaster",
    "links": [
        {
            "href": "/things/toaster/properties",
            "mediaType": "application/json",
            "rel": "properties"
        },
        {
            "href": "/things/toaster/actions",
            "mediaType": "application/json",
            "rel": "actions"
        },
        {
            "href": "/things/toaster/events",
            "mediaType": "application/json",
            "rel": "events"
        }
    ],
    "name": "Acme Toaster",
    "properties": {
        "on": {
            "description": "Whether the toaster is currently heating bread",
            "href": "/things/toaster/properties/on",
            "type": "boolean",
            "unit": ""
        },
        "timeRemaining": {
            "description": "",
            "href": "/things/toaster/properties/timeRemaining",
            "type": "number",
            "unit": "seconds"
        }
    },
    "type": "Toaster"
}
```

- Setting a thing property

```
$ curl localhost:3000/things/toaster/properties/on -XPUT -d '{"on": "true"}'

{
    "on": "true"
}
```

- Getting a thing property

```
$ curl localhost:3000/things/toaster/properties/on

{
    "on": "true"
}
```

Originally posted on the [UnifiedThings blog](https://unifiedthings.github.io/blog/2018/03/19/introducing-vertex/).
