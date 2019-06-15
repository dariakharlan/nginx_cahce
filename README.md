Run nginx
```
docker run --name some-nginx -v ~/projects/nginx_cache/img:/usr/share/nginx/html:ro -v ~/projects/nginx_cache/nginx.conf:/etc/nginx/nginx.conf -v ~/projects/nginx_cache/default.conf:/etc/nginx/conf.d/default.conf -d -p 8080:80 nginx
```


Nginx config for enabling cache
```
http {
    ...
    proxy_cache_path /var/cache levels=1:2 keys_zone=my_cache:10m max_size=10g
                 inactive=60m use_temp_path=off;
}

server {
    ...

    location / {
        ...
        proxy_cache my_cache;
        proxy_cache_min_uses 2;
    }
}
```

Parameter `proxy_cache_min_uses 2` puts file to cache only after it was requested at least 2 times

