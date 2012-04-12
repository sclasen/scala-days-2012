!SLIDE center transition=toss
# An Inside look at Heroku through the lens of Scala
<br/>
![Heroku](logo.png)

Follow along at 
http://scala-days-2012.herokuapp.com

!SLIDE transition=toss
# Me

* Scott Clasen
* Heroku Scala Language Owner
* github.com/ticktock | github.com/sclasen
* @scottclasen

!SLIDE bullets incremental transition=toss
* What is Heroku? 
* How do I deploy to Heroku?
* What's a Procfile?
* What's a Buildpack?
* What's a Config Var?
* What's a Dyno?
* Whats's an Addon?
!SLIDE center 
# What is Heroku? 
!SLIDE center
## Heroku is a polyglot cloud application platform with first class support for Scala, Clojure, Java, Ruby, Python and Node.js
!SLIDE center
## We strive to remove all the operational friction from the development process. 

## We let you just concentrate on coding your app. 

## Code. Deploy. Rinse. Repeat. 

## We manage load balancing, process monitoring, log aggregation and more.

!SLIDE center transition=toss
# How do I deploy to Heroku?
!SLIDE commandline incremental transition=toss
## Deployment to Heroku is done with git.
    
    $ git init
    $ git add .
    $ git commit -m 'initial commit'
    $ heroku create --stack cedar
    Creating blooming-sunrise-8081... done, stack is cedar
    http://blooming-sunrise-8081.herokuapp.com/
    | git@heroku.com:blooming-sunrise-8081.git
    Git remote heroku added
    $ git push heroku master
    ...output from app deployment...code some more...
    $ git commit -a -m 'more changes'
    $ git push heroku master


!SLIDE 
##So now that I've pushed my code 
##How does Heroku know what to run?


!SLIDE center transition=toss
# What's a Procfile?
!SLIDE center transition=toss
# A Procfile is a text file that lets Heroku know the different process types in your app
!SLIDE code transition=toss
## Example (of a project using xsbt-start-script-plugin)

    web: target/start com.myco.myapp.Server

!SLIDE code smaller transition=toss
## Another example

    web: target/start com.myco.myapp.WebServer
    queueReader: target/sart com.myco.myapp.QueueReader
    batchJob1: target/start com.myco.myapp.BatchRunner Job1
    batchJob2: target/start com.myco.myapp.BatchRunner Job2

!SLIDE code smaller transition=toss
## One more Example 

    web: java -cp lib/* -Dweb.port=${PORT} some.main.Clazz

!SLIDE 
## Whats that ${PORT} thing on the last example?


!SLIDE smbullets transition=toss
# What's a Config Var?
##Config Vars are a set of managed environment variables for your app
* ${PORT} is assigned dynamically by the heroku runtime
* All others via 'heroku config:add FOO=bar'
* Every time Config Var state is mutated, a completely new release of your app is created
* Set a bad config var? No worries, 'heroku rollback'


!SLIDE 
## Ok, so what hapens when I push my code?
## How does it get built?


!SLIDE smbullets transition=toss
# What's a Buildpack?
## A buildpack is an adapter between an app and Heroku’s runtime. 
## A buildpack is responsible for language/framework-specific details including:

* Creating the proper runtime environment around the app (e.g. ensuring sbt is downloaded and installed)
* Dependency resolution (e.g via sbt, maven, etc)
* Building the app so that it can execute 'in place'

!SLIDE center transition=toss
# Buildpacks are open source
Scala Buildpack
https://github.com/heroku/heroku-buildpack-scala
## Fork and tweak ours or create your own

heroku create --stack cedar  
--buildpack https://github.com/yourgithub/yourbuildpack.git#somerev


!SLIDE center incremental transition=toss
# What's a Dyno? 

* Dyno is the term for Heroku's abstraction of compute resource
* Essentially a Distributed UNIX process
* Technically a chrooted locked down lxc container

!SLIDE 
# Dyno Features

Elasticity: The number of dynos allocated for your app can be increased or decreased at any time - without any server provisioning.
!SLIDE 
# Dyno Features

Intelligent routing: The routing mesh tracks the location of all web dynos and routes HTTP traffic to them accordingly.
!SLIDE 
# Dyno Features

Process management: Each dyno process is monitored for responsiveness. Misbehaving dynos are taken down and new dynos are launched in their place.
!SLIDE 
# Dyno Features
Distribution and redundancy: Dynos are distributed across a distributed execution environment known as the dyno manifold. An app configured with two web dynos is running two processes, as you’d expect, but each process is running in a separate physical location. If a machine goes down, your site stays up - even with only two dynos.
!SLIDE 
# Dyno Features
Isolation: Every dyno is completely isolated in its own subvirtualized container, with many benefits for security, resource guarantees, and overall robustness.

!SLIDE center transition=toss
# What's an Addon? 






