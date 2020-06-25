# What is Heroku
Heroku is foremost a cloud platform where you can currently push and 
deploy applications built in a variety of languages such as:
- Node
- Ruby
- Java
- PHP
- Python
- Go 
etc.
Heroku considered as plarform as a service where developer can choose
different IT platforms like: servers, databases and runtime environments,
and male them as easy to use as possible. All of this built on AWS.
Heroku consist of 2 basic concepts:
- dyno - is a smart containers that know how to deploy and run specific
technology sych as node server or a Java JVM. They can scaled up and down.
- add-ons - allow you to add other tools and platforms to your dynos. These
can be databases like Postgres, MySQL, logging aggregators, or other tools 
that you would typically utillize to build a modern web.

# Heroku Buildpacks
Buildpacks are set of scripts and files that act kind of like a giant application
compiler and build tool. The buildpack will take all your raw application files 
and prepare it so it's in a state that can be usable as a final application artifact.
It then transforms and compiles your application using the buildpack's inner application
knowledge into what Heroku terms a slug. The slug is then in a state that the dyno knows
how to deploy and serve your finalized application on the Heroku platform. Heroku
provides several officially maintained buildpacks.

# Deployment
In this file contains instruction for each type of language application how to deploy
app to heroku environment.
- Rails
- Django
- Boot			
-> server| this will consist of server-side only apps that expose an API endpoint 
and don't have any kind of UI associated with them. You can call the endpoint and it 
will simply return JSON payload.
- Angular/Node
-> UI Server| It will provide Angular for front-end app, and it will also act as a
server-side app that exposes the same API by using Node. To make it more interestiong
all app will rely on Riverbrain.com site. Riverbrain site like a wikipedia info about
rivers.
So we will pull data from heroku servers which pull data from Riverbrain API.

 
