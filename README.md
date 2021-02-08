# mylyn-gitea

Gitea Mylyn Connector : Gitea Issues management for Eclipse/Mylyn.

This Mylyn connector will allow you to connect Mylyn to a Gitea instance (self hosted or not) in order to manage your issues on Gitea with your local Eclipse instance.

## Thanks and Credits

I want to thanks and credit:

* pweingardt for the "Mylyn Gilab Connector" https://github.com/pweingardt/mylyn-gitlab, the "Mylyn Gitea Connector" is inspired from.
* zeripath for the "Java Gitea API" https://github.com/zeripath/java-gitea-api , used to communicate with Gitea instance.

## Changes 

* 08.02.2021 - I'm currently working to make the connector working, resolving package and installation issues (plugins crash on eclipse start due to missing class Exception), then I will debug basic features (repository connectorion ...) before I will upload first code and binaries.

## Planned Features

### Version 1.x - prove of concept
* use basic (user,password) or token authentication
* list and query for issues
* handles issues on a repository basis

### Version 2.x - usable 
* use basic (user,password) or token authentication
* create, edit, close and reopen issues
* comment on issues
* supports repository milestones and assignees
* handles issues on a repository basis


### Missing features

* Password prompt (I just don't know how...)

### Won't be implemented

The goal of this connector is not to replaced the Gitea web interfac, so everything which is not Issue related or not link with what may help a developper in his day-to-day issue management will not be implemented, typically Team/Repository member management and milestone management.

## Usage

1. Install the plugin obviously (you can use the https://github.com/teilginn/mylyn-gitea update site)
2. Add a new Connector, using the new Gitea Connector
  1. enter the project URL (something like `http(s)://my-gitea-instance.org/myname_or_organisation/myrepository`)
  2. enter your usename and your password 
  3. **Do not forget to check the "Save Password" checkbox**. I don't know how to create a password prompt...
3. You can now create queries and issues

If you use https instead of http (and you absolutely should use https), be sure you have a valid certificate. That means it is signed by a trusted CA. If you don't have a valid certificate (like a self signed certificate), the plugin will refuse to connect. If you want to add your CA certificate to the java keystore, you have to:

1. find the keystore which is used by your JVM (on my machine it is /etc/ssl/certs/java/cacerts)
2. find out the password for the keystore (the default is "changeit")
3. add the CA certificate to this keystore
  1. On Linux, Mac OS X, or Unix systems, use `keytool -import -alias A-UNIQUE-ALIAS -file YOUR-CA.crt -keystore $PATH_TO_YOUR_KEYSTORE` (root permissions may be necessary)
  2. On Windows, in an Administrator Command Prompt use `"%PROGRAMFILES%\java\jre7\bin\keytool" -import -alias A-UNIQUE-ALIAS -file YOUR-CA.cer -keystore "%PROGRAMFILES%\Java\jre7\lib\security\cacerts"`

I don't kown if I will introduce the option to ignore certificate errors. It is not a good way to do those kind of things, especially as it's now not so difficult to get a valid certificate for self hosted services thanks to Let's Encrypt.

## Known issues/Limitations

* List of Eclipse version plugins is compliant is to be defined, It will be test with the version of Eclipse I'm using (Linux/Windows) in front of always an always up to date gitea instance. 
* Version 1.x will only support read acess and queries, we have may to wait the Version 2.x to create and modify issues.
* If you created a new milestone or added a new project member via the web interface, you have to update the repository configuration, so that the connector reloads the project members and milestones. Right click on the Gitea repository in the Task repositories view and click on "Update Repository Configuration".
* Offline mode does not work.
* Out of the box support for valid certificates only.   


