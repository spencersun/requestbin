# We have discontinued the publicly hosted version of RequestBin due to ongoing abuse that made it very difficult to keep the site up reliably. Please see instructions below for setting up your own self-hosted instance.

Originally Created by [Jeff Lindsay](http://progrium.com)

License
-------
MIT


Looking to self-host?
=====================

[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy)

## Deploy your own instance using Heroku
Create a Heroku account if you haven't, then grab the RequestBin source using git:

`$ git clone git://github.com/Runscope/requestbin.git`

From the project directory, create a Heroku application:

`$ heroku create`

Add Heroku's redis addon:

`$ heroku addons:add heroku-redis`

Set an environment variable to indicate production:

`$ heroku config:set REALM=prod`

Now just deploy via git:

`$ git push heroku master`

It will push to Heroku and give you a URL that your own private RequestBin will be running.


## Deploy your own instance using Docker

On the server/machine you want to host this, you'll first need a machine with
docker and docker-compose installed, then grab the RequestBin source using git:

`$ git clone git://github.com/Runscope/requestbin.git`

Go into the project directory and then build and start the containers

```
$ sudo docker-compose build
$ sudo docker-compose up -d
```

Your own private RequestBin will be running on this server.

Misc
====

## Extend the lifetime of a bin

By default bins expire 2 days after creation.  You can examine/manipulate the expiration
for redis-backed bins as follows:

```
# Find out how much time is left
docker exec -it requestbin_redis_1 redis-cli ttl requestbin_xxxxxxxx
(integer) 83601

# Change the expiration to 30 days from now
docker exec -it requestbin_redis_1 redis-cli expire requestbin_xxxxxxxx 2592000
(integer) 1
```

Contributors
------------
 * Barry Carlyon <barry@barrycarlyon.co.uk>
 * Jeff Lindsay <progrium@gmail.com>
