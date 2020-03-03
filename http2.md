# Add HTTP2

Everything was already setup similar to the tutorial. Only added http2 to the listen directive.

```Bash
listen 443 ssl http2 default_server;
listen [::]:443 ssl http2 default_server;
```

## References
* https://www.digitalocean.com/community/tutorials/how-to-set-up-nginx-with-http-2-support-on-ubuntu-16-04
