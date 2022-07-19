# PHP-Practice


steps.
1- Create a repo directory
2- git clone the project
3. use command :  docker-compose up --build -d



## Unique visitors

### What is Sentry?

Sentry is a real-time crash reporting tool that can work with multiple frameworks.

Learn more: [https://www.getsentry.com/welcome/]()  
Github link: [https://github.com/getsentry/sentry]()

### Getting Started

Sentry is releases as a Python pip package. We will use the Python buildpack,
the pip package and add some configuration files to deploy the app.

There is an open source project to deploy Sentry to Heroku here:
[https://github.com/fastmonkeys/sentry-on-heroku](). That project was forked to
create [https://github.com/dlapiduz/sentry-on-cf]().

###Prerequisites
Azure - Virtual Machine with docker engine


### Steps

1. 
1. Clone the  repo:  
`git clone https://github.com/dlapiduz/sentry-on-cf` to the Virtual Machine 
1. Edit the `mani.yml` & update the actions secrets from the respectice Virtual Machine
1. Push the application without starting it to create the environment:  
  `cf push --no-start`
1. Create a postgres database service instance and bind it:  
  For example: `cf create-service rds shared-psql sentrydb`  
  `cf bind-service sentry sentrydb`
1. Create a redis service instance and bind it:  
  For example: `cf create-service redis28-swarm standard sentryredis`  
  `cf bind-service sentry sentryredis`
1. Add the services to your `manifest.yml` file:  

  ```
  ...
  services:
  - sentrydb
  - sentryredis
  ...
  ```
1. Get the Redis URL from the app environment and take note of it:
  `cf env sentry`
1. Set required environment variables in your `manifest.yml` file:  
  (use the Redis settings from the previous step to set REDIS_URL)  

  ```
  env:
    SENTRY_URL_PREFIX: my-sentry.apps.com
    REDIS_URL: redis://dummy:password@1.1.1.1:12345
    SECRET_KEY: secretkeyshhh
    SENTRY_ADMIN_EMAIL: myemail@email.com
    SERVER_EMAIL: theserver@email.com
    MANDRILL_USERNAME:  
    MANDRILL_APIKEY:  
  ```
1. Run `cf-ssh` to ssh into a container to run admin tasks (this might take a while)
1. Once in the container terminal run:  

  ```
  # Fill in the DB
  sentry --config=sentry.conf.py upgrade --noinput
  # Create an account (say yes to superuser)
  sentry --config=sentry.conf.py createuser
  ```
1. Do one more `cf push` to make sure all the apps are up and running

And you should have a working Sentry installation!


<!-- New -->
# My Awesome App
 
## Introduction
What the app is for.
 
## Environment
> Changing the environment? Change the CI/CD pipeline!
 
Install                          | Version    
---------------------------------|------------
.NET Framework                   | 4.8
PowerShell Core                  | 7.x
Visual Studio (recommended)      | VS 2019+
 
Sources:
*   [.NET Framework](https://dotnet.microsoft.com/download/dotnet-framework)
*   [PowerShell Core](https://docs.microsoft.com/en-us/powershell/scripting/install/installing-powershell-core-on-windows)
 
## Getting Started
> Be sure to use the correct versions from above.
 
**Environment**  
1.  Install PowerShell Core [version].
1.  Install .NET Framework [version].
 
**Application** 
    ```powershell
    # Clone source
    cd "C:\users\[user]\source\repos"
    git clone [path-to-repo]
    cd [appname]
    # Build app
    ./build.ps1
    ```
 
## Daily Development
Things needed to smoothly develop, such as how to run service dependencies.
 
## When to run the build script
    ```powershell
    ./build.ps1
    ```
The build script simulates what the CI server will do, and is intended to catch build errors before they get to the server. The script should be run before the "final" PR commit. That is:
 
1.  Before pushing the final feature branch, AND/OR
1.  Before pushing to the mainline branch
 
## Troubleshooting
Things that might go wrong. These SHOULD end up on product backlogs and get fixed.


