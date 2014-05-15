# Plugins

An EnchanTest plugin acts as an interface to a specific programming language or technology. It communicates with EnchanTest through asynchronous, JSON-based messages sent over a socket interface. The plugin translates the generic requests from EnchanTest into the specific programming language or protocol, runs tests and then sends information back (also as JSON-based messages). Since most programming languages supports JSON and sockets it is easy to create a new plugin if one is missing. Below we first describe the main structure of any EnchanTest JSON message and then describe the different JSON messages that a plugin must as well as can support.

## General EnchanTest message format

All EnchanTest messages are formatted in JSON and have the basic format:

  {
    "date": "2014-05-15",
    "time": "09:57:14",
    "messageCount": 1,
    "version": "0.0.1",
    "type": "Message",
    "message": {
      "name": "SomeMessageName"
      // Message specific information goes here...
    } 
  }

The message count, date, and time are updated with each message sent. The version number states the version of EnchanTest in the messages it sends and of the plug-in in its messages. The type can currently only be either "Message" (used for all messages) or "Meta" (for meta messages such as resends etc). Below we show the different messages that a plug-in MUST or CAN implement. We only list the contents of their "message" field.

## MUST messages

### Run test(s) message

All tests have a title and one or more tags. Tags can be hierarchically organized. The run message is used to start the execution of all tests matching a specific tag and/or title:

  {
    "name": "Run",
    "id": 4252452,
    "title": "Test title",
    "tags": ["gui", "feature/RadarMap/*"]
  }

A plug-in will either answer with an "Error" message or with a TestResults message with the results from the running the requested tests.

### Error message

Whenever a plug-in (or EnchanTest itself) does not understand a message or cannot perform an action it will return an error message:

  {
    "name": "Error",
    "responseToId": 4252452,
    "description": "No tests match!",
    "details": {
      // This part will vary depending on the type of error, here an error from a "Run" message
      "title": "Test title from run message",
      "tags": ["tags/from/run/message", "all/tags/will/be/here", "that/were/in/request"]
    }
  }

### TestResult message

When a plug-in

## CAN messages