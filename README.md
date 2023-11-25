# `aquadoggo` deployment resources

An incomplete collection of "playbooks" documenting the required steps for deploying a public
[`aquadoggo`](https://github.com/p2panda/aquadoggo) node.

## Why this?

All p2p networks which connect peers over The Internet require some publicly deployed
infrastructure for aiding in discovery, connectivity between inaccessible peers, and often for
increasing data availability.

If you want to run your own small/medium p2p network, this often means deploying the
infrastructure yourself. Doing this in a reliable and sustainable way can be a pain...

This repository is for collecting common, low-cost, patterns for deploying this infrastructure for
a p2panda network. Specifically, this means deploying an `aquadoggo` node somewhere at a public address.

## Documented deployments

- [] no-platform (basic)
- [] no-platform (system service)
- [] RPi (LAN only)
- [] docker
- [x] dokku
- [x] fly.io
- [] ansible

Note that all the deployments will only include basic configuration of the `aquadoggo` node. You
will need to adjust the configuration to suit your needs, please see the relevant
[`aquadoggo` cli documentation](https://github.com/p2panda/aquadoggo/tree/main/aquadoggo_cli) for detailed instructions.

## Contributions

PRs for not-yet-documented platforms welcome :-]

## Notes
- the scope of this repo could be expanded to include documentation for other p2p networks