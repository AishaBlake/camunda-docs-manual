---

title: "Get Message Event Subscription"
weight: 130

menu:
  main:
    name: "Get"
    identifier: "rest-api-execution-get-message-subscription"
    parent: "rest-api-execution-message-event-subscription"
    pre: "GET `/execution/{id}/messageSubscriptions/{messageName}`"

---


Get a message event subscription for a specific execution and a message name.


# Method

GET `/execution/{id}/messageSubscriptions/{messageName}`


# Parameters

## Path Parameters

<table class="table table-striped">
  <tr>
    <th>Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>id</td>
    <td>The id of the execution that holds the subscription.</td>
  </tr>
  <tr>
    <td>messageName</td>
    <td>The name of the message that the subscription corresponds to.</td>
  </tr>
</table>


# Result

A JSON object with the following properties:

<table class="table table-striped">
  <tr>
    <th>Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>id</td>
    <td>The identifier of the event subscription.</td>
  </tr>
  <tr>
    <td>eventType</td>
    <td>The type of the event. <code>message</code> for message events.</td>
  </tr>
  <tr>
    <td>eventName</td>
    <td>The name of the event the subscription belongs to, as defined in the process model.</td>
  </tr>
  <tr>
    <td>executionId</td>
    <td>The id of the execution the subscription belongs to.</td>
  </tr>
  <tr>
    <td>processInstanceId</td>
    <td>The id of the process instance the subscription belongs to.</td>
  </tr>
  <tr>
    <td>activityId</td>
    <td>The id of the activity that the event subscription belongs to. Corresponds to the id in the process model.</td>
  </tr>
  <tr>
    <td>createdDate</td>
    <td>The time the subscription was created by the engine. Format <code>yyyy-MM-dd'T'HH:mm:ss</code>.</td>
  </tr>
</table>


# Response Codes

<table class="table table-striped">
  <tr>
    <th>Code</th>
    <th>Media type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>200</td>
    <td>application/json</td>
    <td>Request successful.</td>
  </tr>
  <tr>
    <td>404</td>
    <td>application/json</td>
    <td>A message subscription for the given name and execution does not exist.
    This may either mean that the execution does not exist, or that it is not subscribed on such a message.
    See the <a href="{{< ref "/reference/rest/overview/_index.md#error-handling" >}}">Introduction</a> for the error response format.</td>
  </tr>
</table>


# Example

## Request

GET `/execution/anExecutionId/messageSubscriptions/someMessage`

## Response

    {"id": "anEventSubscriptionId",
    "eventType": "message",
    "eventName": "anEvent",
    "executionId": "anExecutionId",
    "processInstanceId": "aProcInstId",
    "activityId": "anActivity",
    "createdDate": "2013-01-23T13:59:43"}

