# Hornet Chrysalis dev-release installation

This simple guide provides instructions for running a Hornet node using `docker` and `docker-compose` connected to the Chrysalis testnet.

**Warning: this node boilerplate is not meant for production use; please modify your setup to meet any security requirements. You probably want to add authentication to your web interface or avoid exposing it externally**

## Requirements

You need the following to get started:

 - A server to run the node on (preferably 4 core / 8GB minimum)
 - `git` installed
 - `docker` installed
 - `docker-compose` installed

## Installation instructions

First we need to build the docker image from the `develop` branch before we can use it:

```
git clone https://github.com/gohornet/hornet.git
cd hornet
git checkout develop
```

Next up we build the docker image and give it the name `hornet:dev`:

```
docker build -f docker/Dockerfile.dev -t hornet:dev .
```

Now we can create our configuration and docker-compose playbook, simply checkout the following boilerplate configuration to a new folder:

```
cd ..
git clone https://github.com/fijter/hornet-testnet-boilerplate.git hornet-docker
cd hornet-docker
```

We will use the boilerplate configuration file as a symlink from the git source:

```
ln -s ../hornet/config_chrysalis_testnet.json ./config.json
```

Adjust any configuration values to your liking in `docker-compose.yml` and `config.json`

## Running the node

Simply run `docker-compose up` in the `hornet-docker` folder and it should spin up the node. The logs should output your new Peering ID; Copy this so others can peer with you.

The multiaddress you need to share needs to have the following format:

```
/ip4/<YOUR_PUBLIC_UP>/tcp/15600/p2p/<YOUR_PEER_ID>
```

Or if you prefer a hostname:

```
/dns/<YOUR.HOSTNAME.COM>/tcp/15600/p2p/<YOUR_PEER_ID>
```

Once you exchanged this info with another node you can both add your peers multiaddress to `peering.json` in the `p2p > peers` section; Once that's done and the nodes are both started you should peer up and sync with the network.
