---

title: "Get Single Historic Detail"
weight: 30

menu:
  main:
    name: "Get"
    identifier: "rest-api-history-get-detail"
    parent: "rest-api-history-detail"
    pre: "GET `/history/detail/{id}`"

---


Retrieves a single historic detail by id.


# Method

GET `/history/detail/{id}`


# Parameters

## Path Parameters

<table class="table table-striped">
  <tr>
    <th>Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>id</td>
    <td>The id of the detail.</td>
  </tr>
</table>

## Query Parameters

<table class="table table-striped">
  <tr>
    <th>Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>deserializeValue</td>
    <td>
      {{< rest-var-query-param-deserialize-object-value >}}
    </td>
  </tr>
</table>

# Result

An object having the following properties:

<table class="table table-striped">
  <tr>
    <th>Name</th>
    <th>Value</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>id</td>
    <td>String</td>
    <td>The id of the historic detail.</td>
  </tr>
  <tr>
    <td>type</td>
    <td>String</td>
    <td>The type of the historic detail. Either <code>formField</code> for a submitted form field value or <code>variableUpdate</code> for variable updates.</td>
  </tr>
  <tr>
    <td>processDefinitionKey</td>
    <td>String</td>
    <td>The key of the process definition that this historic detail belongs to.</td>
  </tr>
  <tr>
    <td>processDefinitionId</td>
    <td>String</td>
    <td>The id of the process definition that this historic detail belongs to.</td>
  </tr>
  <tr>
    <td>processInstanceId</td>
    <td>String</td>
    <td>The id of the process instance the historic detail belongs to.</td>
  </tr>
  <tr>
    <td>activityInstanceId</td>
    <td>String</td>
    <td>The id of the execution the historic detail belongs to.</td>
  </tr>
  <tr>
    <td>executionId</td>
    <td>String</td>
    <td>The id of the execution the historic detail belongs to.</td>
  </tr>
  <tr>
    <td>caseDefinitionKey</td>
    <td>String</td>
    <td>The key of the case definition that this historic detail belongs to.</td>
  </tr>
  <tr>
    <td>caseDefinitionId</td>
    <td>String</td>
    <td>The id of the case definition that this historic detail belongs to.</td>
  </tr>
  <tr>
    <td>caseInstanceId</td>
    <td>String</td>
    <td>The id of the case instance the historic detail belongs to.</td>
  </tr>
  <tr>
    <td>caseExecutionId</td>
    <td>String</td>
    <td>The id of the case execution the historic detail belongs to.</td>
  </tr>
  <tr>
    <td>taskId</td>
    <td>String</td>
    <td>The id of the task the historic detail belongs to.</td>
  </tr>
  <tr>
    <td>time</td>
    <td>String</td>
    <td>The time when this historic detail occurred, has the format <code>yyyy-MM-dd'T'HH:mm:ss</code>.</td>
  </tr>
</table>

Depending on the type of the historic detail it contains further properties. In case of a <code>HistoricVariableUpdate</code> the following properties are also provided:

<table class="table table-striped">
  <tr>
    <th>Name</th>
    <th>Value</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>variableName</td>
    <td>String</td>
    <td>The name of the variable which has been updated.</td>
  </tr>
  <tr>
    <td>variableInstanceId</td>
    <td>String</td>
    <td>The id of the associated variable instance.</td>
  </tr>
  <tr>
    <td>variableType</td>
    <td>String</td>
    <td>{{< rest-var-response-type >}}</td>
  </tr>
  <tr>
    <td>value</td>
    <td>String/Number/Boolean/Object</td>
    <td>{{< rest-var-response deserializationParameter="deserializeValue" >}}</td>
  </tr>
  <tr>
    <td>valueInfo</td>
    <td>Object</td>
    <td>{{< rest-var-response-valueinfo >}}</td>
  </tr>
  <tr>
    <td>revision</td>
    <td>number</td>
    <td>The revision of the historic variable update.</td>
  </tr>
  <tr>
    <td>errorMessage</td>
    <td>String</td>
    <td>An error message in case a Java Serialized Object could not be de-serialized.</td>
  </tr>
</table>

In case of an <code>HistoricFormField</code> the following properties are also provided:

<table class="table table-striped">
  <tr>
    <th>Name</th>
    <th>Value</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>fieldId</td>
    <td>String</td>
    <td>The id of the form field.</td>
  </tr>
  <tr>
    <td>fieldValue</td>
    <td>String/Number/Boolean/Object</td>
    <td>The submitted value.</td>
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
    <td>Variable with given id does not exist. See the <a href="{{< ref "/reference/rest/overview/_index.md#error-handling" >}}">Introduction</a> for the error response format.</td>
  </tr>
</table>


# Example

## Request

GET `/history/detail/someId`

## Response

Status 200.

```json
{
  "id": "12345",
  "processInstanceId": "aProcInstId",
  "activityInstanceId": "anActInstId",
  "executionId": "anExecutionId",
  "caseInstanceId": null,
  "caseExecutionId": null,
  "time": "2014-02-28T15:00:00",
  "variableName": "myProcessVariable",
  "variableInstanceId": "aVariableInstanceId",
  "variableType": "String",
  "value": "aVariableValue",
  "revision": 1,
  "errorMessage": null
}
```
