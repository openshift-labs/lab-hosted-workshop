---
Title: Hosted Workshop
PrevPage: 01-workshop-spawner
NextPage: ../finish
---

The different configurations supported by the workshop spawner provide different capabilities and behaviour. The sections below go into more details about different aspects of how the `hosted-workshop` configuration works so it can be compared to other configurations. By comparing these to other configurations you can determine if this configuration is the best one for the type of workshop you want to run.

#### User Access

Users attending the workshop would need to be allocated a user name to use in the OpenShift cluster in advance of trying to access the workshop environment. When accessing the workshop environment they will be presented with the login page for the OpenShift cluster. Once they login with the user name and password they were provided, they will be redirected to the workshop environment.

#### Shell Terminal

A shell terminal is provided in the web browser. Command line tools for accessing the cluster, such as `oc`, `odo` and `kubectl` are provided, and configuration is setup in advance so those tools will talk to the cluster the workshop environment is running in.

In order that the user is automatically logged into the cluster from the command line, the spawner when deployed will need to be provided with a table for the user names and passwords. This is needed as the OpenShift OAuth provider doesn't provide an access token which allows the full access a user would have. Thus the login names and passwords have to be provided to the spawner if you want users to be automatically logged in.

If the login names and passwords cannot be supplied, the user will need to run `oc login` to login to the cluster from the command line before using any of the command line tools to work with the cluster.

#### Web Console

An embedded web console is provided if the spawner is provided with the login names and passwords. If they aren't the embedded web console will be disabled and not visible. In this case, the user would need to use a separate browser window or tab to visit the main URL for the OpenShift cluster web console.

#### Cluster Access

Once logged in, the user is able to do anything to the OpenShift cluster that the user they were allocated would be permitted to do. What they can do is therefore dictated by the global cluster policies or specific constraints applied to the users or any group they are a member of.

#### Default Project

If login names and passwords were provided to the spawner, a default project to use for that user can also be supplied, with the project being created if it doesn't exist.

#### Cluster Admin

A user would only have cluster admin access if that user was given the role of a cluster admin, or if they had sudoers role. If they were only granted sudoers role and not cluster admin, then the web console would only provide access based on what they as a user could do, and not what sudoer access from the command line provided.

#### Resource Quotas

Resources quotas and limit ranges that apply to the user and/or projects they create, are dictated by any global configuration, or limit ranges applied by a project template when a project was created.

#### User Storage

The local file system accessible from the terminal is ephemeral. Persistent storage can optionally be enabled, in which case the users workspace within the file system will be preserved if the container running the workshop environment is restarted.

#### Session Timeout

The user can take as long as they like to do the workshop, there is no time restriction. If however the user closes the browser window, or their computer goes to sleep, the container for their workshop environment will be shutdown after an idle timeout period. Because the hosted workshop configuration might be used for all day workshops, the default idle timeout is 2 hours, to allow for a long lunch.

#### Spawner Admin

Specific users can be designated as an admin for accessing the spawner admin panel. This would usually only be granted to the user that the course supervisor used. The admin panel will allow that user to see the list of users connected and stop the users session if necessary. The admin can also impersonate a user so they can view their terminal sessions.
