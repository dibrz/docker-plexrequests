![https://linuxserver.io](http://www.linuxserver.io/wp-content/uploads/2015/06/linuxserver_medium.png)

The [LinuxServer.io](https://www.linuxserver.io/) team brings you another quality container release featuring easy user mapping and 
community support. Be sure to checkout our [forums](https://forum.linuxserver.io/index.php) or for real-time support our 
[IRC](https://www.linuxserver.io/index.php/irc/) on freenode at `#linuxserver.io`.

# lsiodev/plexrequests

![](https://raw.githubusercontent.com/linuxserver/beta-templates/master/lsiodev/img/plexrequests-banner.png)

Simple automated way for users to request new content for Plex Users can search for content to request. Integrates with couchpotato, sonarr 
and sickrage etc... [Plexrequests](http://plexrequests.8bits.ca/)

## Usage

```
docker create --name=plexrequests -v /etc/localtime:/etc/localtime:ro
-v \ <path to data>:/config -e PGID=<gid> -e PUID=<uid>  \
-p 3000:3000 lsiodev/plexrequests
```

**Parameters**

* `-p 3000` - the port(s)
* `-v /etc/localtime` for timesync - *optional*
* `-v /config` - where plexrequests should store its config files
* `-e PGID` for GroupID - see below for explanation
* `-e PUID` for UserID - see below for explanation
* `-e URL_BASE` - used for reverse proxy, see below for explanation

It is based on phusion-baseimage with ssh removed, for shell access whilst the container is running do `docker exec -it plexrequests 
/bin/bash`.

### User / Group Identifiers

**TL;DR** - The `PGID` and `PUID` values set the user / group you'd like your container to 'run as' to the host OS. This can be a user 
you've created or even root (not recommended).

Part of what makes our containers work so well is by allowing you to specify your own `PUID` and `PGID`. This avoids nasty permissions 
errors with relation to data volumes (`-v` flags). When an application is installed on the host OS it is normally added to the common group 
called users, Docker apps due to the nature of the technology can't be added to this group. So we added this feature to let you easily 
choose when running your containers.

## Setting up the application

Webui is at `<your-ip>:3000` , sign in with your plex username. More info from the plexrequest website here 
[FAQ](http://plexrequests.8bits.ca/faq/).

If you need to use a reverse proxy for plexrequest, set `URL_BASE` to `/<name>`
The / before the name is important.
## Info

* To monitor the logs of the container in realtime `docker logs -f plexrequests`.



## Versions

+ **05.02.2016:** Initial Release.

