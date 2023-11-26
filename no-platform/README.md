# No Platform

# deployment

## prerequisites:

- a linux server with a static ip address which you can SSH into with the sudo privileges

## commands

```bash
# open udp port 2022 which is required for replication traffic and tcp port 2020 which is required for http requests.
sudo ufw allow 2020/tcp
sudo ufw allow 2022/udp

# download and unarchive the correct aquadoggo binary for your system (check the releases page to see all available 
# pre-compiled binaries https://github.com/p2panda/aquadoggo/releases)
wget https://github.com/p2panda/aquadoggo/releases/download/v0.7.0/aquadoggo-v0.7.0-x86_64-unknown-linux-gnu.tar.gz
tar -xvzf aquadoggo-v0.7.0-x86_64-unknown-linux-gnu.tar.gz

# create a file named `config.toml` where we will copy the config from this repo.
touch config.toml
# COPY THE CONTENTS OF THE config.toml IN THIS DIRECTORY INTO THIS FILE #

# open a new screen session named "aqudoggo" (screen is a terminal multiplexer, we use it so we can close our SSH 
# session with the server without stopping the running aquadoggo process, read more here: https://linux.die.net/man/1/screen)
screen -S aquadoggo

# start aquadoggo! It will read and apply the configurations from the config.toml file.
./aquadoggo

# you can exit the screen session without stopping the aquadoggo process by typing: Ctrl+a d
# you can enter the screen session later by typing: screen -r aquadoggo
```

The only changes (from the default) made to the `config.toml` file are:
- setup persistent storage locations
- enable info level logs
- enable relay mode

If we ran this only using command line args, it would look like:

```bash
./aquadoggo --log-level info \
            --private-key "$HOME/.local/share/aquadoggo/private-key.txt" \
            --database-url "sqlite:$HOME/.local/share/aquadoggo/db.sqlite3" \
            --blobs-base-path "$HOME/.local/share/aquadoggo/blobs" \ 
            --relay-mode true
```

# caveats

Depending on your os there may be system dependencies missing which `aquadoggo` requires, these
will need installing before you can proceed.

# cost

Any ongoing costs associated with your server host will of course apply. These vary depending on
provider, you don't need a powerful server though, in my experience the lowest level normally will
be enough.

# comments

If you already have access to a server then this is by far the quickest/easiest way to get
running. It is, of course, a little fragile, and it would be hard to keep track of many services
deployed on the same server in this way (that's what platforms are for ;-p). But there are ways of
making it more manageable, and having automatic restarts when things go wrong. Tell me your tales!