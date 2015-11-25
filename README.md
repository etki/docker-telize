# Telize in Docker

This repository contains Docker image definition for [Telize][] service.

Telize is a very simple (and beautiful!) lua-scripted nginx configuration that
provides JSON REST API for retrieving GeoIP information about particular IP
address. Because it is simply nothing but a nginx config with a little Lua
flavour, it provides fantastic throughput (3000+ rps on my 300$ notebook).

## Usage

### Launch your dockers, skipper

    docker run -d -p 80:80 --name telize etki/telize
    
### Backtracking that bastard by IP

Simply GET <telize-host>/geoip/<ip>. More information can be found at
[official documentation][telize]

    curl localhost/geoip/8.8.8.8

### What's next

I'm no sysadmin or nginx expert, so configuration, probably, have lots of
headroom for tuning. Also, amount of workers (which should be equal to processor
cores amount) is hardcoded to 2, so in most cases you'll want to set it to more
than just 2 - to do that, simply inherit from this image and overwrite
`/etc/nginx/nginx.conf` with your own settings. I have plans for cleaning
everything up and placing sed'ding bash wrapper script that will reconfigure
container on every start, but don't have any time for this yet.

Oh, and that last thing: by default there is no access log, and error log goes
strictly to stderr.

### Licensing

- [Telize][telize-license]
- [Docker][docker-license]
- [Maxmind geoip databases][maxmind-license]

  [telize]: http://www.telize.com/
  [telize-license]: https://github.com/fcambus/telize/blob/master/LICENSE
  [docker-license]: https://github.com/docker/docker/blob/master/LICENSE
  [maxmind-license]: http://dev.maxmind.com/geoip/legacy/geolite/#License