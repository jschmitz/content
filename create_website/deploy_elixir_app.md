# Deploy an Elixir application with NGINX

# WIP

This is a walkthrough of deploying what is my third incaration of my recent website. The following will be used:
* Digital Ocean Ubuntu Droplet
* NGINX
* Elixir
* Phoenix
* Postgres

## Phoenix Releases

Follow these steps

    * https://hexdocs.pm/mix/Mix.Tasks.Release.html


## Install Postgres to your Droplet

TODO add pg instructions

## Phoenix Release Continued

Now you have postgres installed and the other configs all set.  Time to run the release.

Release created at

```Bash


_build/prod/rel/jakeschmitz3!

    # To start your system
    _build/prod/rel/jakeschmitz3/bin/jakeschmitz3 start

Once the release is running:

    # To connect to it remotely
    _build/prod/rel/jakeschmitz3/bin/jakeschmitz3 remote

    # To stop it gracefully (you may also send SIGINT/SIGTERM)
    _build/prod/rel/jakeschmitz3/bin/jakeschmitz3 stop

To list all commands:

    _build/prod/rel/jakeschmitz3/bin/jakeschmitz3
```


This is was important in the config. The site did not display until this was added.

@todo need to explain what is happening

```Elixir
config :phoenix, :serve_endpoints, true
```

### Run your app as a Daemon

_build/prod/rel/jakeschmitz3/bin/jakeschmitz3 daemon

### Netstat

On Ubuntu the following netstat command will show you the port and the pid that your app is running on.
`
netstat -ltnp
`

The outbput will have entries similar to the following to allow you to confirm the port is active by mapping the pid to the process.

```Bash
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp6       0      0 :::4000                 :::*                    LISTEN      30142/beam.smp
```

You can find the pid of your app with


```Bash
_build/prod/rel/jakeschmitz3/bin/jakeschmitz3 pid
```

To stop your application server process:

`
kill -9 <your-pid>
`

## Configure nginx

Once the app is up and running you can use nginx to point to the port that was made available.

```Bash
location /new {
  rewrite ^/new(.*) /$1 break;
  proxy_pass http://127.0.0.1:4000;
}
```

Notice the rewrite rule applied. The route that will used to access the new site will be /new and the rewrite rule will proxy the request to the elixir app as removing "new".  This will allow phoenix app as if it were executing at the root.






## References
* https://hexdocs.pm/mix/Mix.Tasks.Release.html
* https://geoffreylessel.com/2016/hosting-a-phoenix-app-in-a-subdirectory-with-nginx/
* https://www.cyberciti.biz/faq/nginx-restart-ubuntu-linux-command/
