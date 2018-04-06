---
layout: post
title: Introducing Vertex
---

[Vertex](https://github.com/unifiedthings/vertex) is (will be) an implementation of [Web Thing API specification](https://unifiedthings.github.io/mozilla-wot-spec) by [Mozilla IoT](https://iot.mozilla.org). In layman's terms it will be the software package which will run and power the Internet of Things (IoT) edge nodes or devices. The name 'vertex' signifies an edge running on the internet. Many such 'vertex' nodes will run together in a network to form an Edge Computing Network and provide services in a de-centralized fashion on the internet.

The rest of the post will cover how to build, install and run vertex on a node. Please note that vertex is still under active development and the prototype will miss many specifications. We will keep on updating this post as and when we add new features and capabilities.

#### Dependencies

- python

#### Build Instructions

- Get the python dependencies

```
$ pip install -r requirements.txt
```

#### Running the Thing API Server

```
$ python vertex.py server [port]
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
  },
  "events": {
    "ready": {
      "description": "Your toast is ready!"
    }
  },
  "actions": {
    "pop": {
      "description": "Pop up the toast",
      "input": {
         "type": "number"
       },
      "callable": "echo Popping up these many toasts"
    }
  }
}
```

- Import using the vertex executable

```
$ python vertex.py import toaster /path/to/toaster-schema.json
```

#### Using the Web Thing API

- Get a list of all things

```
$ curl localhost:3000/things
 
[
  {
    "actions": {
      "pop": {
        "description": "Pop up the toast",
        "href": "/things/toaster/actions/pop",
        "input": {
          "type": "number"
        }
      }
    },
    "description": "A web connected toaster",
    "events": {
      "ready": {
        "description": "Your toast is ready!",
        "href": "/things/toaster/events/ready",
        "type": null,
        "unit": null
      }
    },
    "links": [
      {
        "href": "/things/toaster/properties",
        "mediaType": "application/json",
        "rel": "properties"
      },
      {
        "href": "/things/toaster/events",
        "mediaType": "application/json",
        "rel": "events"
      },
      {
        "href": "/things/toaster/actions",
        "mediaType": "application/json",
        "rel": "actions"
      }
    ],
    "name": "Acme Toaster",
    "properties": {
      "on": {
        "description": "Whether the toaster is currently heating bread",
        "href": "/things/toaster/properties/on",
        "maximum": null,
        "minimum": null,
        "type": "boolean",
        "unit": null
      },
      "timeRemaining": {
        "description": null,
        "href": "/things/toaster/properties/timeRemaining",
        "maximum": null,
        "minimum": null,
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
  "actions": {
    "pop": {
      "description": "Pop up the toast",
      "href": "/things/toaster/actions/pop",
      "input": {
        "type": "number"
      }
    }
  },
  "description": "A web connected toaster",
  "events": {
    "ready": {
      "description": "Your toast is ready!",
      "href": "/things/toaster/events/ready",
      "type": null,
      "unit": null
    }
  },
  "links": [
    {
      "href": "/things/toaster/properties",
      "mediaType": "application/json",
      "rel": "properties"
    },
    {
      "href": "/things/toaster/events",
      "mediaType": "application/json",
      "rel": "events"
    },
    {
      "href": "/things/toaster/actions",
      "mediaType": "application/json",
      "rel": "actions"
    }
  ],
  "name": "Acme Toaster",
  "properties": {
    "on": {
      "description": "Whether the toaster is currently heating bread",
      "href": "/things/toaster/properties/on",
      "maximum": null,
      "minimum": null,
      "type": "boolean",
      "unit": null
    },
    "timeRemaining": {
      "description": null,
      "href": "/things/toaster/properties/timeRemaining",
      "maximum": null,
      "minimum": null,
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

- Requesting an action

```
$ curl localhost:3000/things/toaster/actions -XPOST -d '{"pop": {"input": 10}}'

{
  "pop": {
    "href": "/things/toaster/actions/pop/a4a4aec2-1fa2-4abf-ace7-86bdf8e6e47b",
    "input": 10,
    "status": "pending"
  }
}
```

- Getting the actions queue

```
$ curl localhost:3000/things/toaster/actions

[
  {
    "pop": {
      "href": "/things/toaster/actions/pop/32ddeb33-bdc2-42d2-9bed-c5f5d0a2678a",
      "input": "12",
      "status": "completed",
      "timeCompleted": "2018-04-06 15:21:00.394353",
      "timeRequested": "2018-04-06 15:21:00.382574"
    }
  },
  {
    "pop": {
      "href": "/things/toaster/actions/pop/a4a4aec2-1fa2-4abf-ace7-86bdf8e6e47b",
      "input": "10",
      "status": "completed",
      "timeCompleted": "2018-04-06 15:20:21.675748",
      "timeRequested": "2018-04-06 15:20:21.665374"
    }
  }
]
```

- Getting the action status

```
$ curl localhost:3000/things/toaster/actions/pop/32ddeb33-bdc2-42d2-9bed-c5f5d0a2678a

{
  "pop": {
    "href": "/things/toaster/actions/pop/32ddeb33-bdc2-42d2-9bed-c5f5d0a2678a",
    "input": "12",
    "status": "completed",
    "timeCompleted": "2018-04-06 15:21:00.394353",
    "timeRequested": "2018-04-06 15:21:00.382574"
  }
}
```

- Pushing an event

```
$ curl localhost:3000/things/toaster/events -XPOST -d '{"ready": {"data": true}}'

{
  "ready": {
    "data": true
  }
}
```

- Getting the event log

```
$ curl localhost:3000/things/toaster/events

[
  {
    "ready": {
      "data": "True",
      "timestamp": "2018-04-06 15:23:08.115557"
    }
  }
]
```

Originally posted on the [UnifiedThings blog](https://unifiedthings.github.io/blog/2018/03/19/introducing-vertex/).
