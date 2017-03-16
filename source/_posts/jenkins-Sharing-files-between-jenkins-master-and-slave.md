title: '[jenkins] Sharing files between jenkins master and slave nodes'
author: lyenliang
date: 2017-03-16 20:37:10
tags:
---
Sometimes you may want to share files between your jenkins master and slave nodes. 

For example, maybe I have a powershell script, `test.ps1`, which contains some frequently called functions.

	# test.ps1

	function foo {
	  echo "bar"
	}
    

One way to share this file is save it at master, and copy it to slave node before it is called by slave node. This would require many jenkins configurations. 

Recently I found that this can be easily done with [Config File Provider Plugin](https://wiki.jenkins-ci.org/display/JENKINS/Config+File+Provider+Plugin).

First you need to install the plugin. After it is installed, you can find `Managed files` at `http://JENKINS_URL/manage`. Click it.

<img src="/images/jenkins/Managed_files.png" alt="Managed files" style="width: 630px; "/>

Then define your shared file by clicking `Add a new Config` -> `Custom file`

<img src="/images/jenkins/Add_a_new_Config.png" alt="Add a new Config" style="width: 630px; "/>

<img src="/images/jenkins/custom_file.png" alt="Custom file" style="width: 630px; "/>

Now you are going to define the name and content of the shared file.

<img src="/images/jenkins/content.png" alt="Custom file" style="width: 630px; "/>

Now the file is ready to be used by your jenkins projects. 

Inside your project, you can find a `Provide Configuration files` option. Check it.

<img src="/images/jenkins/Provide_Configuration_files.png" alt="Custom file" style="width: 630px; "/>

Let's take a look at the options here. *File* means the shared file you just defined.

Jenkins will create the *File* at the folder specified by *Target* (In my case, I specify the folder to be the workspace of my project). 

Remember to make sure that the folder exists before building the project.

*Variable* represents an environment variable with which you can refer to the file.

Now you can import this file no matter whether you are at master or slave node.

<img src="/images/jenkins/Build.png" alt="Import Excute" style="width: 630px; "/>

`. $env:util` imports the file. This makes powershell recognize `foo` command.