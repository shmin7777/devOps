``` 
server {
    listen       80;
    server_name  localhost;
    server_name  192.168.87.42;


    #access_log  /var/log/nginx/host.access.log  main;

    root  /ncp/data/www/;
    index index.html index.htm;
    location / {
      try_files $uri $uri/ = 404; # uri 경로에서 찾고 없으면 404
      proxy_pass http://3.36.131.2:8081; # reverse proxy
    }

    error_page  404              /404.html;

    # redirect server error pages to the static page /50x.html
    #
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /ncp/data/www;
      # root  /usr/share/nginx/html;
    }

    # proxy the PHP scripts to Apache listening on 127.0.0.1:80
    #
    #location ~ \.php$ {
    #    proxy_pass   http://127.0.0.1;
    #}

    # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
    #
    #location ~ \.php$ {
    #    root           html;
    #    fastcgi_pass   127.0.0.1:9000;
    #    fastcgi_index  index.php;
    #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
    #    include        fastcgi_params;
    #}

    # deny access to .htaccess files, if Apache's document root
    # concurs with nginx's one
    #
    #location ~ /\.ht {
    #    deny  all;
    #}
}

```
