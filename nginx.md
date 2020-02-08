# NGINX
The plan is to use NGINX to pass http request to multiple servers as needed. The current plan is to setup a simple proxy server traffic bettween an Elixir Phoenix application and a tbd blog hosting software.  This post has a nice walk through of getting setup: https://medium.com/@a4word/setting-up-phoenix-elixir-with-nginx-and-letsencrypt-ada9398a9b2c and in the beginners guide you (https://nginx.org/en/docs/beginners_guide.html) can see more information in the section Setting Up a Simple Proxy Server.

## Ubuntu config file location server locations
* /etc/nginx/nginx.conf
* /etc/nginx/sites-enabled/

## Start and Stop NGINX

* sudo systemctl start nginx
* sudo systemctl stop nginx

## Debugging

Use the journalctl -xe and the logs are pretty verbose and once you locate the error message its helpful. An example useful chunk of errors would look like:

```bash
Feb 08 13:09:56 nginx: [emerg] host not found in upstream "your_app_upstream" in /etc/nginx/sites-enabled/app.com:11
Feb 08 13:09:56 nginx[27308]: nginx: configuration file /etc/nginx/nginx.conf test failed
Feb 08 13:09:56 systemd[1]: nginx.service: Control process exited, code=exited, status=1/FAILURE
```

## Netstat
Verify your app is running at the port you specified:

```bash
netstat -ltnp
tcp6       0      0 :::4001                 :::*                    LISTEN      1869/beam.smp
```

## References
* https://nginx.org/en/docs/
* https://nginx.org/en/docs/beginners_guide.html
* https://medium.com/@a4word/setting-up-phoenix-elixir-with-nginx-and-letsencrypt-ada9398a9b2c
* https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/
* https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/#passing-a-request-to-a-proxied-server
