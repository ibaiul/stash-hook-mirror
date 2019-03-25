# Bitbucket Server Repository Hook for Mirroring (Englishtown fork)

The following is a plugin for Atlassian Bitbucket Server to provide repository mirroring to a remote repository.

Tested and working correctly on Bitbucket 6.0.0

## Notice

I have forked the original [repository](https://github.com/ef-labs/stash-hook-mirror) for my personal use since the original author has not committed in more than a year and after updating my Bitbucket instance to 6.0.0 the plugin was not supported anymore.

I committed the minimum changes required to adapt it to Bitbucket 6.0.0.

Many, many thanks to [@Englishtown](http://www.englishtown.com) for the great contribution.

This repository does not pretend to replace the original work in any way and I do not have the intention to maintain or publish this in the Atlassian market, instead I will provide the necessary steps to build your own version with the minimum changes required to make it work in Bitbucket +6.0.0 in case you need to use it before the original author can update his work or merge any pull requests.

## Steps

Below you will find the required steps to build a jar file that contains the modified version of the plugin that makes it compatible with Bitbucket +6.0.0. Once the jar is built, you will be able to upload it to your own Bitbucket instances and start using it.

##### Install Atlassian SDK (RPM / RHEL / CentOS / Fedora (Yum))

Install Java 8

```
sudo yum install jdk
```

Create repository definition file

```
sudo nano /etc/yum.repos.d/artifactory.repo
```
Copy the content below

```
[Artifactory]
name=Artifactory
baseurl=https://packages.atlassian.com//atlassian-sdk-rpm/
enabled=1
gpgcheck=0
```
Install the SDK

```
sudo yum clean all
sudo yum updateinfo metadata
sudo yum install atlassian-plugin-sdk
```
##### Install Atlassian SDK (other platforms)

https://developer.atlassian.com/server/framework/atlassian-sdk/downloads/

##### Clone this repository

Check the commits and if you trust my changes then proceed. The default branch is called **ibai**

```
git clone https://github.com/ibaiul/stash-hook-mirror.git
```
##### Change pom.xml

Optionally you can edit the pom.xml file to adapt the artifactId, groupId, repositories, etc. to match your organization.

##### Build your artifact

To build your own artifact go to the folder where pom.xml file is located and build it.

```
cd <path_where_you_cloned_this_repo>
atlas-mvn clean package
```
If everything went correctly you can grab your plugin jar file at the target folder.

```
ls -l target/stash-hook-mirror-${version}.jar
```
##### Use my artifact

If you don't feel on the mood of building your own jar file, you can get the version I built for myself, although I would recommend building your own jar from the source code since you can always audit it.

You should not use artifacts built from unknown sources since you never know what it could be inside. That said, if you want to proceed, you can get my artifact [here](https://nexus.ibai.eus/repository/maven-releases-public/eus/ibai/stash-hook-mirror/2.4.0/stash-hook-mirror-2.4.0.jar).

##### Install the plugin

Browse your Bitbucket instance as admin and click on "Administration" (top right corner) -> "Manage apps" (Addons section) -> "Upload app" -> Select the jar file you just built.

Now you should be able to enable the plugin in your repositories under the "Repository Settings" -> "Hooks" section.
