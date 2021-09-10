[hub]: https://hub.docker.com/r/mightydetail/fivem
[git]: https://github.com/Andruida/fivem

# [mightydetail/fivem][hub] <img align="right" height="250px" src="https://portforward.com/fivem/fivem-logo.png">

This docker image allows you to run a server for FiveM, a modded GTA multiplayer program.
This image includes [txAdmin](https://github.com/tabarra/txAdmin), an in-browser server management software.
Upon first run, the configuration is generated in the host mount for the `/config` directory, and for the `/txData` directory (that contains the txAdmin configuration).

[dockerhub]: https://hub.docker.com/r/mightydetail/fivem
[github]: https://github.com/mightydetail/docker-fivem
[![](https://images.microbadger.com/badges/image/mightydetail/fivem.svg)](https://microbadger.com/images/mightydetail/fivem)
[![Latest Version](https://images.microbadger.com/badges/version/mightydetail/fivem.svg)][dockerhub]
[![Docker Pulls](https://img.shields.io/docker/pulls/mightydetail/fivem.svg)][dockerhub]
[![Docker Stars](https://img.shields.io/docker/stars/mightydetail/fivem.svg)][dockerhub]

## Licence Key

A freely obtained licence key is required to use this server, which should be declared as `FIVEM_LICENCE_KEY`. A tutorial on how to obtain a licence key can be found [here](https://forum.fivem.net/t/explained-how-to-make-add-a-server-key/56120)

## Usage

Use the docker-compose script as provided:

```sh
---      
version: '2'
services:
# -------------------------------------------------------------------
  fivem:
    container_name: fivem
    image: mightydetail/fivem:dev
    stdin_open: true
    tty: true
    volumes:
      # Remember to change.
      - /opt/fivem/resources:/config
      - /opt/fivem/txdata:/txData
    ports:
      - 30120:30120
      - 30120:30120/udp
      - 40120:40120
    environment:
      TZ: Europe/Berlin
      SERVER_PROFILE: default
      FIVEM_PORT: 30120
      WEB_PORT: 40120
      HOST_UID: 1000
      HOST_GID: 1000
      # Remember to change.
      FIVEM_HOSTNAME: FiveM
```

_It is important that you use `interactive` and `pseudo-tty` options otherwise the container will crash on startup_
See [issue #3](https://github.com/spritsail/fivem/issues/3)

### Environment Varibles

| **Variable name** | **Description** | **Value** |
|---|---|---|
| TXADMIN_PORT | Port used for getting to txAdmin webgui. Will be used in the server.cfg. | 40120 |
| FIVEM_PORT | Port used to connect to the FiveM Server. Will be used in the server.cfg. |  30120 |
| FIVEM_HOSTNAME | This will be the FiveM Server name in game. Will be used in the server.cfg.  | FiveMESX Game |

- `RCON_PASSWORD` - A password to use for the RCON functionality of the fxserver. If not specified, a random 16 character password is assigned. This is only used upon creation of the default configs
- `HOST_GID` - The files that are generated by the container will be written with this group ID. You must use numeric IDs. If not specified, will use `0` (root).
- `HOST_UID` - The files that are generated by the container will be written with this user ID. You must use numeric IDs. If not specified, will use `0` (root).
- `SERVER_PROFILE` - profile name used by txAdmin. If not specified, will use `dev_server`.

## Credits 
<img align="right" height="200px" src="https://raw.githubusercontent.com/tabarra/txAdmin/master/docs/banner.png">

 - Thanks to **tabarra** as the creator and maintainer of the [txAdmin](https://github.com/tabarra/txAdmin) repository!
 - Thanks to [henkall][git] that I forked this code from
