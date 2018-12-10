nix-bitcoin
===

Nix packages and nixos modules including profiles to easily install featureful Bitcoin nodes.
Work in progress.

Profiles
---
`nixbitcoin.nix` provides the two profiles "minimal" and "all":

* minimal
    * bitcoind (pruned) with outbound connections through Tor and inbound connections through a hidden
      service
    * [clightning](https://github.com/ElementsProject/lightning) with outbound connections through Tor, not listening
    * includes "nodeinfo" script which prints basic info about the node
    * adds non-root user "operator" which has access to bitcoin-cli and lightning-cli
* all
    * adds clightning hidden service
    * [liquid-daemon](https://github.com/blockstream/liquid)
    * [lightning charge](https://github.com/ElementsProject/lightning-charge)
    * [nanopos](https://github.com/ElementsProject/nanopos)
    * adds an index page using nginx to display node information and link to nanopos
    * [spark-wallet](https://github.com/shesek/spark-wallet)
        * Notes: run `nodeinfo` to get its onion address and `systemctl status spark-wallet` to get the access key.
            When entering the onion address on the Android app don't forgot to prepend "http://"

The data directories can be found in `/var/lib`.

Installing profiles
---
The easiest way is to use the provided network.nix and configuration.nix with [nixops](https://nixos.org/nixops/manual/).
Once you've set up nixops first run `./generate_secrets.sh` then continue with the deployment using nixops.

At the moment this relies on using the unstable nixpkgs channel.
The "all" profile requires 15 GB of disk space and 2GB of memory.
