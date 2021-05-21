# Using a reverse proxy

The use of nginx as a reverse proxy for stash is possible. 
A sample configuration of headers that need to be set mentioned [here](https://github.com/stashapp/stash/pull/134) is 

```nginx
location / {
    proxy_pass http://127.0.0.1:9999;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $remote_addr;
    proxy_set_header X-Forwarded-Port $server_port;
    proxy_set_header X-Forwarded-Proto $scheme;
}
```

As of commit `7767271`, if needed you can adjust the `external_host` setting to your external address as mentioned [here](https://github.com/stashapp/stash/pull/369)

In order for the websocket to work, you may need to also add these lines to your server block (`proxy.conf` file in the Let's Encrypt Unraid docker container for instance) as mentioned [here](https://github.com/stashapp/stash/issues/532)

```nginx
proxy_http_version 1.1;
proxy_set_header Upgrade $http_upgrade;
proxy_set_header Connection "upgrade";
```

If you are using the linuxserver letencrypt docker you can use create a `stash.subdomain.conf` file in your `proxy-confs` folder and use this as the config:

```nginx
# make sure that your dns has a cname set for stash

server {
    listen 443 ssl;
    listen [::]:443 ssl;

    server_name stash.*;

    include /config/nginx/ssl.conf;

    client_max_body_size 0;

    # enable for ldap auth, fill in ldap details in ldap.conf
    #include /config/nginx/ldap.conf;

    location / {
        # enable the next two lines for http auth
        #auth_basic "Restricted";
        #auth_basic_user_file /config/nginx/.htpasswd;

        # enable the next two lines for ldap auth
        #auth_request /auth;
        #error_page 401 =200 /login;

        include /config/nginx/proxy.conf;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        resolver 127.0.0.11 valid=30s;
        set $upstream_app stash;
        set $upstream_port 9999;
        set $upstream_proto http;
        proxy_pass $upstream_proto://$upstream_app:$upstream_port;
    }

}
```

Another example for `nginx`:

In this case we are using `stash.home` as our domain and `192.168.0.1` is stash's ip so edit accordingly.

The `external_host` configuration option should also be set, in this case `external_host: http://stash.home`. Refer to [external_host](https://github.com/stashapp/stash/pull/369) for more details

```nginx
server {
    listen 80;
    listen [::]:80;

    server_name stash.home;
        client_max_body_size 0;
        location / {
           proxy_pass http://192.168.0.1:9999/;
           proxy_http_version 1.1;
           proxy_set_header Upgrade $http_upgrade;
           proxy_set_header Connection "Upgrade";
           proxy_set_header Host $host;
           proxy_set_header X-Real-IP $remote_addr;
           proxy_set_header X-Forwarded-For $remote_addr;
           proxy_set_header X-Forwarded-Port $server_port;
           proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```