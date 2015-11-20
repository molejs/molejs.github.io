# Mole log specification

All log reports sent to the mole server and processed by the mole dashboard follow a common structure, that is, the **Mole log specification**.

## Log object

The main log object where all the data is contained.

Field | Type | Description
--- | --- | ---
`id` | string | ID of the log, must not be present on the report but is on the retrieval
`timestamp` | string | Timestamp of the report
`location` | Location object | URL location where the error happened
`action_state_history` | Array of ActionState objects | An array with the pairs of action-state that lead to the error
`error` | Error object | Information about the error such as the line and the stacktrace

## Location object

The location object contains all the information about the URL where the error happened.

Field | Type | Description
--- | --- | ---
`host` | string | Host of the page
`href` | string | Full URL of the page
`hash` | string | Hash of the page
`pathname` | string | Path name of the page
`port` | string | Port of the page
`protocol` | string | Protocol of the page
`search` | string | Search query of the page

## Error object

The error object contains all the data of the error, which is the message and the stacktrace.

Field | Type | Description 
--- | --- | ---
`message` | string | Message of the error
`stacktrace` | Array of StackTrace objects | Stacktrace of the error

## Stacktrace object

The stacktrace object contains all the data of a stacktrace line.

Field | Type | Description
--- | --- | ---
`function` | string | Function of the stacktrace line
`file` | string | File of the stacktrace line
`line` | string | Line of the stacktrace line
`column` | string | Column of the stacktrace line

## ActionState object

The ActionState object contains the pair of action and state.

Field | Type | Describe
--- | --- | ---
`action` | Arbitrary JSON Object | The action that happened in that entry
`state` | Arbitrary JSON Object | The state of the application at the moment the action happened

## Example log

```
{
  "id": "55bb692e19ff303084000004",
  "timestamp": "Fri Nov 20 2015 13:55:06 GMT+0100 (CET)",
  "location": {
    "host": "fake.molejs.org",
    "href": "http://fake.molejs.org/app",
    "hash": "",
    "pathname": "/app",
    "port": "",
    "protocol": "http:",
    "search": ""
  },
  "error": {
    "message": "TypeError: undefined is not a function",
    "stacktrace": [
      {
        "function": "emit",
        "file": "events.js",
        "line": "107",
        "column": "17"
      },
      {
        "function": "EventEmitter.<anonymous>",
        "file": "index.js",
        "line": "170",
        "column": "9"
      },
      {
        "function": "EventEmitter.emit",
        "file": "events.js",
        "line": "107",
        "column": "17"
      },
      {
        "function": "ClientRequest.<anonymous>",
        "file": "index.js",
        "line": "50",
        "column": "7"
      }
    ]
  },
  "action_state_history": [
    {
      "action": {
        "type": "OPEN_PRODUCT",
        "product": 45,
      },
      "state": {

      }
    },
    {
      "action": {
        "type": "LOAD_PRODUCT",
        "product": 45
      },
      "state": {
        "currentProduct": 45
      }
    },
    {
      "action": {
        "type": "PRODUCT_LOADED"
      },
      "state": {
        "currentProduct": 45,
        "loading": true,
      }
    },
    {
      "action": {
        "type": "DISPLAY_PRODUCT"
      },
      "state": {
        "currentProduct": 45,
        "product": {
          "id": 45,
          "name": "Foo flowers",
          "image": "foo_flowers.jpg",
          "price": 34.45
        },
        "loading": false,
      }
    }
  ]
}
```
