MisterNote API
==============


General notes
-------------

  * All API requests can be done via **Socket.IO** framework, raw **WebSocket** protocol or **HTTP REST API** (unless otherwise specified).

  * All values are required (unless otherwise specified).

  * URLs for requests are:
      * `/api/socketio/` for Socket.IO;
      * `/api/websocket/` for raw WebSocket;
      * `/api/rest/` for HTTP REST.


Socket.IO and WebSocket
-----------------------

  * Each outgoing and incoming messages are **JSON** objects with keys and values described in this file.

  * API comminucation IS NOT necessarily a request-response sequence. If client sent a request, it doesn't mean that next message from server would be a response to that request. Here is an example of this situation:
    * client sent `get_note` request;
    * server sent `update` event message (there were some changes in user notes right after this request, e.g. added new note from other device);
    * server sent `get_note` response.

  * But for each request server will send a reply eventually (and again, it should not necessarily be right after request message).


HTTP REST API
-------------

  * Each request is an HTTP GET request.

  * HTTP response contains reply for the request.

### Event messages with HTTP REST API
  * To get *event messages*, client should send `ping` request:

Key | Value
----|------
`type` | `ping`

  * Reply would contain exactly one unread event if any exist:

Key | Value
----|------
`type` | `update` or any other event type
... | ...

  * If there are none unread events, server will return `pong` response:

Key | Value
----|------
`type` | `pong`


TODO
----

  * OAuth (VK, Facebook, Twitter, Google+)
  * Errors descriptions
  * E-mail confirmation
  * File uploading
