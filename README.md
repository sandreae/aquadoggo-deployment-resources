# `aquadoggo` deployment resources

An incomplete collection of "playbooks" documenting the required steps for deploying a public
[`aquadoggo`](https://github.com/p2panda/aquadoggo) node using a variety of common methods.

## Why this?

All p2p networks which connect peers over The Internet require some publicly deployed
infrastructure for helping peers discover each other and form stable connections. In some cases
they are also used for improving data availability.

If you want to run your own small/medium p2p network, this often means someone deploying and
maintaining this infrastructure. Doing this in a reliable and sustainable way can be a pain...
Even using familiar tools there can be time consuming hidden pitfalls.

With this repository I aim to document deployment of an `aquadoggo` node for a p2panda network
(which performs the above mentioned functions) on some of the most common platforms (and
no-platforms). Hopefully it will be a useful resource for others.

## Documented deployments

- [x] no-platform (basic)
- [ ] no-platform (system service)
- [ ] RPi (LAN only)
- [ ] docker
- [x] dokku
- [x] fly.io
- [ ] ansible

Note that all the deployments will only include basic configuration of the `aquadoggo` node. You
will need to adjust the configuration to suit your needs, please see the relevant
[`aquadoggo` cli documentation](https://github.com/p2panda/aquadoggo/tree/main/aquadoggo_cli) for detailed instructions.

## Contributions

The list of deployment methods above is not exhaustive, just those that came to mind, please
suggest more which could be added to the TODO list.
PRs for not-yet-documented platforms welcome :-]
If spot any mistakes please let me know (or fix them for me...)