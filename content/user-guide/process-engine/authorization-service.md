---

title: 'Authorization Service'
weight: 240

menu:
  main:
    identifier: "user-guide-process-engine-authorization-service"
    parent: "user-guide-process-engine"

---

Camunda BPM provides a resource oriented authorization framework.


# Authorizations

An Authorization assigns a set of Permissions to an identity to interact with a given Resource.

**Examples**

* User 'jonny' is authorized to create new users
* Group 'marketing' is not authorized to delete the Group 'sales'
* Group 'marketing' is not allowed to use the tasklist application.


# Identities

Camunda BPM distinguished two types of identities: users and groups. Authorizations can either range over all users (userId = ANY), an individual User or a Group of users.


# Permissions

A Permission defines the way an identity is allowed to interact with a certain resource.

{{< note title="Buit-In Permissions" class="info" >}}
  The following permissions are currently supported by the authorization framework:

  * None
  * All
  * Read
  * Update
  * Create
  * Delete
  * Access
  * Read Task
  * Update Task
  * Create Instance
  * Read Instance
  * Update Instance
  * Delete Instance
  * Read History
  * Delete History

{{< /note >}}

Please note that the permission "None" does not mean that no permissions are granted, it stands for "no action".
Also, the "All" permission will vanish from a user if a single permission is revoked.

A single authorization object may assign multiple permissions to a single user and resource:

```java
authorization.addPermission(Permissions.READ);
authorization.addPermission(Permissions.UPDATE);
authorization.addPermission(Permissions.DELETE);
```

On top of the built-in permissions, Camunda BPM allows using custom permission types.


# Resources

Resources are the entities the user interacts with.

The following resources are available:

<table class="table matrix-table table-condensed table-hover table-bordered">
  <tr>
    <th>Resource Name</th>
    <th>Integer representation</th>
    <th>Resource Id</th>
  </tr>
  <tr>
    <td>Application (Cockpit, Tasklist, ...)</td>
    <td>0</td>
    <td>admin/cockpit/tasklist/*</td>
  </tr>
  <tr>
    <td>Authorization</td>
    <td>4</td>
    <td>Authorization Id</td>
  </tr>
  <tr>
    <td>Decision Definition</td>
    <td>10</td>
    <td>Decision Definition Key</td>
  </tr>
  <tr>
    <td>Deployment</td>
    <td>9</td>
    <td>Deployment Id</td>
  </tr>
  <tr>
    <td>Filter</td>
    <td>5</td>
    <td>Filter Id</td>
  </tr>
  <tr>
    <td>Group</td>
    <td>2</td>
    <td>Group Id</td>
  </tr>
  <tr>
    <td>Group Membership</td>
    <td>3</td>
    <td>Group Id</td>
  </tr>
  <tr>
    <td>Process Definition</td>
    <td>6</td>
    <td>Process Definition Key</td>
  </tr>
  <tr>
    <td>Process Instance</td>
    <td>8</td>
    <td>Process Instance Id</td>
  </tr>
  <tr>
    <td>Task</td>
    <td>7</td>
    <td>Task Id</td>
  </tr>
  <tr>
    <td>User</td>
    <td>1</td>
    <td>User Id</td>
  </tr>      
</table>

**Note:** The Resource Id should be '*' when you create new authorization with CREATE permissions only.

On top of the built-in resources, the Camunda BPM framework supports defining custom resources. Authorization on custom resources will not be automatically performed by the framework but can be performed by a process application.


# Combination of authorizations and resources

Not every possible permission can be granted for every possible resource.
For the "Application" resource you can exclusively grant the "Access" permission.

The valid combinations can be found in the following table.

<table class="table matrix-table table-condensed table-hover table-bordered">
<thead>
  <tr>
    <th></th>
    <th>Read</th>
    <th>Update</th>
    <th>Create</th>
    <th>Delete</th>
    </tr>
  </thead>
  <tbody>
     <tr>
      <th>Authorization</th>
      <td>X</td>
      <td>X</td>
      <td>X</td>
      <td>X</td>
    </tr>
    <tr>
      <th>Decision Definition</th>
      <td>X</td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>Deployment</th>
      <td>X</td>
      <td></td>
      <td>X</td>
      <td>X</td>
    </tr> 
    <tr>
      <th>Filter</th>
      <td>X</td>
      <td>X</td>
      <td></td>
      <td>X</td>
    </tr>   
    <tr>
      <th>Group</th>
      <td>X</td>
      <td>X</td>
      <td>X</td>
      <td>X</td>
    </tr>
    <tr>
      <th>Group Membership</th>
      <td></td>
      <td></td>
      <td>X</td>
      <td>X</td>
    </tr>  
    <tr>
      <th>Process Definition</th>
      <td>X</td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>Process Instance</th>
      <td>X</td>
      <td>X</td>
      <td>X</td>
      <td>X</td>
    </tr>
    <tr>
      <th>Task</th>
      <td>X</td>
      <td>X</td>
      <td>X</td>
      <td>X</td>
    </tr> 
    <tr>
      <th>User</th>
      <td>X</td>
      <td>X</td>
      <td>X</td>
      <td>X</td>
    </tr>    
  </tbody>
</table>

## Additional Authorizations for Process Definition

* Read Task
* Update Task
* Create Instance
* Read Instance
* Update Instance
* Delete Instance
* Read History
* Delete History
  
## Additional Authorizations for Decision Definition

* Create Instance
* Read History
* Delete History

The "Create Instance" permission is required for evaluating decisions with the decision service.

# Authorization Type

There are three types of authorizations:

Global Authorizations (`AUTH_TYPE_GLOBAL`) range over all users and groups (`userId = ANY`) and are usually used for fixing the "base" permission for a resource.
Grant Authorizations (`AUTH_TYPE_GRANT`) range over users and groups and grant a set of permissions. Grant authorizations are commonly used for adding permissions to a user or group that the global authorization revokes.
Revoke Authorizations (`AUTH_TYPE_REVOKE`) range over users and groups and revoke a set of permissions. Revoke authorizations are commonly used for revoking permissions to a user or group the the global authorization grants.


# Authorization Precedence

Authorizations may range over all users, an individual user or a group of users or they may apply to an individual resource instance or all instances of the same type (resourceId = ANY). The precedence is as follows:

* An authorization applying to an individual resource instance precedes over an authorization applying to all instances of the same resource type.
* An authorization for an individual user precedes over an authorization for a group.
* A Group authorization precedes over a GLOBAL authorization.
* A Group REVOKE authorization precedes over a Group GRANT authorization.

## Create an Authorization

An authorization is created between a user/group and a resource. It describes the user/group's permissions to access that resource. An authorization may express different permissions, such as the permission to READ, UPDATE, DELETE the resource. (See Authorization for details).

In order to grant the permission to access a certain resource, an authorization object is created. For example, to give access to a certain filter:

```java
Authorization auth = authorizationService.createNewAuthorization(AUTH_TYPE_GRANT);

// The authorization object can be configured either for a user or a group:
auth.setUserId("john");
//  -OR-
auth.setGroupId("management");

//and a resource:
auth.setResource("filter");
auth.setResourceId("2313");
// a resource can also be a process definition
auth.setResource(Resources.PROCESS_INSTANCE);
// the process defintion key is the resource id
auth.setResourceId("invoice");

// finally the permissions to access that resource can be assigned:
auth.addPermission(Permissions.READ);
// more than one permission can be granted
auth.addPermission(Permissions.CREATE);

// and the authorization object is saved:
authorizationService.saveAuthorization(auth);
```

As a result, the given user or group will have permission to READ the referenced Filter.

Another possible example would be to restrict the group of persons who are allowed to start a special process:

```java
//we need to authorizations, one to access the process definition and another one to create process instances
Authorization authProcessDefinition = authorizationService.createNewAuthorization(AUTH_TYPE_GRANT);
Authorization authProcessInstance = authorizationService.createNewAuthorization(AUTH_TYPE_GRANT);

authProcessDefinition.setUserId("johnny");
authProcessInstance.setUserId("johnny");

authProcessDefinition.setResource(Resources.PROCESS_DEFINITION);
authProcessInstance.setResource(Resources.PROCESS_INSTANCE);
//the resource id for a process definition is the process definition key
authProcessDefinition.setResourceId("invoice");
//asterisk to allow the start of a process instance
authProcessInstance.setResourceId("*")
// allow the user to create instances of this process definition
authProcessDefinition.addPermission(Permissions.CREATE_INSTANCE);
// and to create processes
authProcessInstance.addPermission(Permissions.CREATE);

authorizationService.saveAuthorization(authProcessDefinition);
authorizationService.saveAuthorization(authProcessInstance);
```

## The Administrator Authorization Plugin

Camunda BPM has no explicit concept of "administrator". An administrator in Camunda BPM is a user who has been granted all authorizations on all resources.

When downloading the Camunda BPM distribution, the invoice example application creates a user with id `demo` and assigns administrator authorizations to this user. In addition, the [Camunda Admin web application]({{< ref "/webapps/admin/user-management.md#initial-user-setup" >}}) allows you to create an initial administrator user if no user is present in the database (when using the [Database Identity Service]({{< ref "/user-guide/process-engine/identity-service.md#the-database-identity-service" >}}) or a custom implementation providing READ / UPDATE access to the user repository).

This is not the case when using the [LDAP Identity Service]({{< ref "/user-guide/process-engine/identity-service.md#the-ldap-identity-service" >}}). The LDAP identity service only has read access to the user repository and the "Create Initial User" dialog will not be displayed.

In this case you can use the *Administrator Authorization Plugin* for making sure administrator authorizations are created for a particular LDAP User or Group.

The following is an example of how to configure the Administrator Authorization Plugin in bpm-platform.xml / processes.xml:

```xml
<process-engine name="default">
  ...
  <plugins>
    <plugin>
      <class>org.camunda.bpm.engine.impl.plugin.AdministratorAuthorizationPlugin</class>
      <properties>
        <property name="administratorUserName">admin</property>
      </properties>
    </plugin>
  </plugins>
</process-engine>
```

The plugin will make sure that administrator authorizations (ALL permissions) are granted on all resources whenever the process engine is started.

{{< note title="" class="info" >}}
  It is not necessary to configure all LDAP users and groups which should have administrator authorization. It is usually enough to configure a single user and use that user to log into the webapplication and create additional authorizations using the User Interface.
{{< /note >}}

Complete list of configuration properties:

<table class="table table-striped">
  <tr>
    <th>Property</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>administratorUserName</code></td>
    <td>The name of the administrator user. If this name is set to a non-null and non-empty value, the plugin will create user-level Administrator authorizations on all built-in resources.</td>
  </tr>
  <tr>
    <td><code>administratorGroupName</code></td>
    <td>The name of the administrator group. If this name is set to a non-null and non-empty value, the plugin will create group-level Administrator authorizations on all built-in resources.</td>
  </tr>
</table>
