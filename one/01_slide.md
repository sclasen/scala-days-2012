!SLIDE center
# Twelve Factor Ruby
<img src="ruby_logo.gif" style="background: white"/>
<br/>
![Heroku](logo.png)

!SLIDE center
<img src="12factor.png" style="background: white"/>
## www.12factor.net
## Adam Wiggins

!SLIDE 
# Me

* Chris Continanza
* Rails 1, 2, 3, Sinatra, CGI.out
* adapters, workers, tests - oh my!
* github.com/csquared
* @em_csquared 


!SLIDE center 
# This is not a talk

<img src="Magritte-pipe.jpg" />

!SLIDE center
# I. Codebase
### One codebase tracked in revision control, 
### many deploys

<img src="codebase-deploys.png" style="background: white"/>

!SLIDE commandline
# II. Dependencies
## Explicitly declare and isolate dependencies

    $ bundle install

    $ bundle exec

!SLIDE
# III. Config
## Store config in the environment

    @@@ Ruby
    Sequel.connect ENV['DATABASE_URL']

    ActiveRecord.establish_connection 
    ActiveRecord.establish_connection(url) 

`https://github.com/glenngillen/activerecord_url_connections `

!SLIDE center
# IV. Backing Services
## Treat backing services as attached resources

### 'URLs are the Uniform Way to Locate Resources' - Adam Wiggins
<img src="attached-resources.png" style="background:white" width="600px"/>

!SLIDE center
# V. Build, release, run
## Strictly separate build and run stages

<img src="release.png" style="background:white" />

!SLIDE commandline
# VI. Processes
## Execute the app as one or more stateless processes

    $ bundle exec thin start

    $ bundle exec rake work

!SLIDE
# VII. Port binding
## Export services via port binding

    $ bundle exec thin start -p $PORT

!SLIDE center
# VIII. Concurrency
## Scale out via the process model

<img src="process-types.png" style="background:white" />

!SLIDE
# IX. Disposability  
## Maximize robustness with fast startup and graceful shutdown

    @@@ Ruby
    trap('SIGTERM') do
      gracefully_shutdown
    end

!SLIDE 
# X. Dev/prod parity
## Keep development, staging, and production as similar as possible

    $ heroku addons:add \
        heroku-postgresql:crane \ 
        --fork postgres://A42...

    $ heroku db:pull



!SLIDE
# XI. Logs
## Treat logs as event streams

    @@@ Ruby
    config.logger = Logger.new(STDOUT)
  
!SLIDE
# Logging Add-ons

  - New relic
  - Hoptoad/Airbrake
  - Papertrail
  - More...

!SLIDE
# XII. Admin Processes
## Run admin/management tasks as one-off processes

    $ bundle exec rake db:migrate

!SLIDE
# (13) Tests 
## Write tests to verify your logic

!SLIDE bullets incremental
# Rails Fails: 
  - III. Config 
  - XI.  Logs

!SLIDE
# III. Config
  
    - config/database.yml
    - config/environments

!SLIDE commandline
# XI. Logs

    $ tail -f log/production.log
    
    $ tail -f log/development.log

!SLIDE
# Both Fails are EASILY overcome

    @@@ Ruby
    config.logger = Logger.new(STDOUT)

    ActiveRecord.establish_connection(
                        ENV['DATABASE_URL'])

!SLIDE bullets
# Gains

- maximum portability / new devs
- deploy on cloud platforms
- continuous deployment  staging
- effortless scale

!SLIDE
# Ruby Frameworks are 
# For The Win!

!SLIDE
# Thank You !

## csquared@heroku.com
## @em_csquared
## github.com/csquared
![Heroku](logo.png)
