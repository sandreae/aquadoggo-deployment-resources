# `dokku`

https://dokku.com/

> Dokku is an extensible, open source Platform as a Service that runs on a single server of your choice. Dokku supports building apps on the fly from a git push via either Dockerfile or by auto-detecting the language with Buildpacks, and then starts containers based on your built image. Using technologies such as nginx and cron, Web processes are automatically routed to, while background processes and automated cron tasks are also managed by Dokku.

# deployment

## prerequisites:

- server running a [dokku](https://dokku.com/) instance which:
  - already has required ports open
  - uses the default nginx proxy plugin
  - has a global domain configured

## commands

On your dokku host machine run the following commands:

```bash
# create the dokku application named `aquadoggo`
dokku apps:create aquadoggo

# instantiate the app with the latest pre-built aquadoggo docker image pulled from docker hub
dokku git:from-image aquadoggo p2panda/aquadoggo:latest

# we need persistent storage for our private key, SQLite database and blobs
dokku storage:ensure-directory --chown false aquadoggo
dokku storage:mount aquadoggo /var/lib/dokku/data/storage/aquadoggo:/app/data

# proxy http traffic from host port 80 to container port 2020 where the http server is listening
dokku ports:set aquadoggo http:80:2020

# retrieve and install TLS certificates for
dokku letsencrypt:enable aquadoggo

# dokku doesn't support setting proxy ports for UDP traffic so we do that via `docker-options` args
dokku docker-options:add aquadoggo deploy -p 2022:2022/udp

# unfortunately customizing the docker run command (above) means we need to disable zero-downtime
#deploys in order to avoid port conflicts on rebuild.
dokku checks:disable aquadoggo

# configure the node via environment variables
dokku config:set aquadoggo BLOBS_BASE_PATH=/app/data DATABASE_URL=sqlite:/app/data/db.sqlite3 LOG_LEVEL=debug PRIVATE_KEY=/app/data/secret.txt
```

Your aquadoggo http endpoints will now be available at `https://aquadoggo.<YOUR_GLOBAL_DOMAIN>`

# cost

dokku is free open-source software, you can provision an instance yourself at no cost. You do need
a server where you can run your dokku instance though, this will come with monthly costs according
to whichever host you choose.

# comments

If you don't already have a dokku instance running then I wouldn't recommend this method, it's
overkill\* (unless you're interested in exploring dokku anyway...).

_\*not to dis dokku, I really like it and use it a lot_
