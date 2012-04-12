!SLIDE 
## Ok, Ok, show me some Scala!

!SLIDE
#Toolbelt

[https://toolbelt.heroku.com/](https://toolbelt.heroku.com/)

Everything you need to get started with heroku.

OR

If you have git, ruby, and gems instaled

gem install heroku

!SLIDE
# Hello Scala on Heroku
[https://github.com/heroku/devcenter-scala](https://github.com/heroku/devcenter-scala)

git clone https://github.com/heroku/devcenter-scala

heroku create --stack cedar

git push heroku master

heroku open

You just deployed your first heroku scala app.

!SLIDE
# A Production Scala app
[https://github.com/heroku/s3pository](https://github.com/heroku/s3pository)

Maven/Ivy-SBT repository proxy server, S3 storage.

Finagle Server.

Used to help speed all Scala, Java, Play builds on Heroku.

Addons: Loggly, New Relic, Heroku Scheduler.

!SLIDE
# heroku.jar 

java/scala client lib for the Heroku API.

[https://github.com/heroku/heroku.jar](https://github.com/heroku/heroku.jar)

Pluggable HTTP Clients. 

(apache-httpclient, ning-async, finagle, play-ws)

(will add spray once ssl client support is in)

Pluggable Futures! 

!SLIDE
# BYO HttpClient and Future
[AsyncConnection interface](https://github.com/heroku/heroku.jar/blob/master/heroku-api/src/main/java/com/heroku/api/connection/AsyncConnection.java)

[FinagleConnection -> Twitter Future](https://github.com/heroku/heroku.jar/blob/master/heroku-http-finagle/src/main/scala/com/heroku/api/connection/FinagleConnection.scala)

[PlayWSConnection -> Play Promise](https://github.com/heroku/heroku.jar/blob/master/heroku-http-play/src/main/scala/com/heroku/api/connection/PlayWSConnection.scala)


















