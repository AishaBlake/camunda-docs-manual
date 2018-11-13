---

title: "Get Historic Details"
weight: 10

menu:
  main:
    name: "Get List"
    identifier: "rest-api-history-get-detail-query"
    parent: "rest-api-history-detail"
    pre: "GET `/history/detail`"

---


Query for historic details that fulfill the given parameters.
The size of the result set can be retrieved by using the [count]({{< ref "/reference/rest/history/detail/get-detail-query-count.md" >}}) method.


# Method

GET `/history/detail`


# Parameters

## Query Parameters

<table class="table table-striped">
  <tr>
    <th>Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>processInstanceId</td>
    <td>Filter by process instance id.</td>
  </tr>
  <tr>
    <td>executionId</td>
    <td>Filter by execution id.</td>
  </tr>
  <tr>
    <td>activityInstanceId</td>
    <td>Filter by activity instance id.</td>
  </tr>
  <tr>
    <td>caseInstanceId</td>
    <td>Filter by case instance id.</td>
  </tr>
  <tr>
    <td>caseExecutionId</td>
    <td>Filter by case execution id.</td>
  </tr>
  <tr>
    <td>variableInstanceId</td>
    <td>Filter by variable instance id.</td>
  </tr>
  <tr>
    <td>tenantIdIn</td>
    <td>Filter by a comma-separated list of tenant ids.</td>
  </tr>
  <tr>
    <td>formFields</td>
    <td>Only include <strong>HistoricFormFields</strong>. Value may only be <code>true</code>, as <code>false</code> is the default behavior.</td>
  </tr>
  <tr>
    <td>variableUpdates</td>
    <td>Only include <strong>HistoricVariableUpdates</strong>. Value may only be <code>true</code>, as <code>false</code> is the default behavior.</td>
  </tr>
  <tr>
    <td>excludeTaskDetails</td>
    <td>Excludes all task-related <strong>HistoricDetails</strong>, so only items which have no task id set will be selected. When this parameter is used together with <code>taskId</code>, this call is ignored and task details are <strong>not</strong> excluded. Value may only be <code>true</code>, as <code>false</code> is the default behavior.</td>
  </tr>
  <tr>
    <td>sortBy</td>
    <td>Sort the results by a given criterion. Valid values are <code>processInstanceId</code>, <code>variableName</code>, <code>variableType</code>, <code>variableRevision</code>, <code>formPropertyId</code>, <code>time</code> or <code>occurrence</code> and <code>tenantId</code>.
    Must be used in conjunction with the <code>sortOrder</code> parameter.</td>
  </tr>
  <tr>
    <td>sortOrder</td>
    <td>Sort the results in a given order. Values may be <code>asc</code> for ascending order or <code>desc</code> for descending order.
    Must be used in conjunction with the <code>sortBy</code> parameter.</td>
  </tr>
  <tr>
    <td>firstResult</td>
    <td>Pagination of results. Specifies the index of the first result to return.</td>
  </tr>
  <tr>
    <td>maxResults</td>
    <td>Pagination of results. Specifies the maximum number of results to return. Will return less results if there are no more results left.</td>
  </tr>
  <tr>
    <td>deserializeValues</td>
    <td>
      {{< rest-var-query-param-deserialize-object-value >}}
    </td>
  </tr>
</table>


# Result

A json array of historic detail objects.
Each historic detail object has the following properties:

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
    <td>tenantId</td>
    <td>String</td>
    <td>The id of the tenant that this historic detail belongs to.</td>
  </tr>
  <tr>
    <td>time</td>
    <td>String</td>
    <td>The time when this historic detail occurred has the format <code>yyyy-MM-dd'T'HH:mm:ss</code>.</td>
  </tr>
</table>

Depending on the type of the historic detail it contains further properties. In case of an <code>HistoricVariableUpdate</code> the following properties are also provided:

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
    <td>{{< rest-var-response deserializationParameter="deserializeValues" >}}</td>
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
    <td>400</td>
    <td>application/json</td>
    <td>Returned if some of the query parameters are invalid, for example if a <code>sortOrder</code> parameter is supplied, but no <code>sortBy</code>. See the <a href="{{< ref "/reference/rest/overview/_index.md#error-handling" >}}">Introduction</a> for the error response format.</td>
  </tr>
</table>


# Example

## Request

GET `/history/detail?processInstanceId=aProcInstId`

## Response

```json
[
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
    "errorMessage": null,
    "tenantId": null
  },
  {
    "id": "12345",
    "processInstanceId": "aProcInstId",
    "activityInstanceId": "anActInstId",
    "executionId": "anExecutionId",
    "caseInstanceId": null,
    "caseExecutionId": null,
    "taskId": "aTaskId",
    "time": "2014-02-28T15:00:00",
    "fieldId": "aFieldId",
    "fieldValue": "aFieldValue",
    "tenantId": null
  }
]
```
