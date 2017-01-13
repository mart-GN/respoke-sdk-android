Respoke Android SDK Change Log
==============================

v1.5.0
------
* Moved RespokeClient.getGroupHistories() to a new route from a deprecated one.
* Adds RespokeClient.getConversations() and .setConversationsRead() for server-side message history support.

v1.4.1
------
* Updated AndroidAsync dependency to 2.1.7

v1.4.0
------

* Added support for retrieving group message history, and marking a message to be persisted
to the history. See commit 9a3f4e6 for details.

v1.3.3
------

* Removed unnecessary inclusion of Google Play Services. The SDK doesn't actually use it. Client 
apps should refer to the demo app for examples of how to use GCM (which relies on Google Play 
Services).

v1.3.2
------

* Fixed a crash that can occur intermittently during call setup

v1.3.1
------

* Fixed a crash that can occur if a hangup signal is received during key moments of call set up

v1.3.0
------

* Improved ice candidates signaling, resulting in faster call setup and inter-op support for
clients that do not support trickle ice, such as chan_respoke.

v1.2.0
------

* Added Respoke-SDK header to websocket & http[s] requests, which includes the sdk version
and the Android OS version making the request.

v1.1.2
------

* Fixed a packaging problem that was preventing the SDK from being installed from Maven

v1.1.1
------

* Added missing in-line documentation to the public interfaces used by client applications.

* Rearranged internally used methods for clarity

v1.1.0
------

* This version of the Android SDK now uses a customized version of the AndroidAsync library 
dependency as a submodule rather than has a Gradle dependency. If you are working with the SDK 
code directly, note that you now need to use the `--recursive` flag when cloning the repository as 
described in the README.

* ***breaking*** Changed the `RespokeEndpoint.sendMessage()` method to now have 4 params,
where the 3rd param is now `Boolean ccSelf`. This param indicates to the Respoke service whether the
message should be sent to other connections of the sender's endpointId or not.

* ***breaking*** Changed the `onMessage()` method of the `RespokeClient.Listener` interface to now require
a 5th param, `Boolean didSend`. This param indicates to the listener whether the message received
was *from* the localEndpoint *sent to* the specified endpoint (didSend=false), or was *from* the
specified endpoint *sent to* the localEndpoint (didSend=true). This change was required to support
messages that could be coming from another connection of the same endpointID that the current client
is connected as (ccSelf).

* ***breaking*** Changed the `onMessage()` method of the `RespokeEndpoint.Listener` interface to now
require a 4th param, `Boolean didSend`. This param has the same meaning as the one added to
`RespokeClient.Listener#onMessage`.

* Added conference call support. Call the new `RespokeClient.joinConference()` method to create a 
RespokeCall instance that will join the multiparty audio conference specified by the conferenceID 
parameter.

* Declining an incoming call by calling the `RespokeCall.hangup()` method in the Android SDK will now also decline that call on any other clients that have logged in to Respoke using the same endpoint ID (Android or otherwise)

* Fixed a bug that could prevent the SDK from registering for push notifications.

* Fixed several intermittent crashes related to hanging up a call.

* Fixed a crash that can occur when an application using the Respoke SDK is pushed into or restored 
from the background.

v1.0.4
------

* Added a new "push" parameter to `RespokeGroup.sendMessage()` and `RespokeEndpoint.sendMessage()`
that allows you to indicate if a specific message should be considered (true) or ignored (false) by
the push notification service. Use this to explicitly ignore certain messages (like meta data) that
should never be sent to mobile devices as a push notification.

* Added a new `Respoke.unregisterPushServices()` method that allows you to explicitly unregister a
device from receiving push notifications in the future.

* Updated the AndroidAsync, Google Play Services, and App Support dependency libraries to the latest
available versions

* Improved the instructions in the README on how to run the SDK test cases

* Miscellaneous test case fixes
