# `fly.io`

https://fly.io/

> Fly is a platform for running full stack apps and databases close to your users. We’ve been
> hammering on this thing since 2017, and we think it’s pretty great. 

(☝️ good for you! ;-p)

# deployment

## prerequisites:

- [fly cli](https://fly.io/docs/flyctl/) installed on your local machine
- fly.io account (or create it in the flow below)

## commands

In the same directory where your `fly.toml` config file is located, on your local machine, run the
following command:

```bash
# only needs to be done once, creates a fly.io account and logs in
fly auth signup

# deploy the app based on the fly.toml configuration
# the `--ha=false` flag means only one machine will be deployed (the default is 2)
fly deploy --ha=false
```

That's actually it, which impressed me a lot!

# caveats

Big caveat is that support for UDP traffic is fairly idiosyncratic on fly.io. The requirement is
that your listening UDP service binds to a special `fly-global-services` address. This currently
isn't possible to do in `aquadoggo` without making changes to the source code, at which point it
is no longer an "easy" deployment. My personal experience is that i _do_ see connections establish
over UDP when binding to `0.0.0.0`, but it's quite unstable.

The issue and solution is explained here: https://fly.io/docs/app-guides/udp-and-tcp/

Also, on the free tier, you are only allowed a "shared" ip4 address, and UDP isn't supported (by
fly.io) for ip6 addresses yet. I'm not sure if the shared ip4 address causes other issues around
exposing UDP.

# cost

fly.io charges based on actual resource used (in/out bound traffic, memory use, storage used
etc..), below a certain threshold it's free though, so if you have a low-traffic instance it's
very possible to deploy a no-cost instance (when there is no traffic, apps are paused and consume
no resources). Of course, this comes with the danger of unwanted fees if you have unexpectedly
high levels of traffic. I believe it's possible to set pay-caps to prevent this though.

# comments

If the above caveat around UDP port configuration is solved then this would be a great way to
quickly set-up testing/small project/temporary nodes very easily.
