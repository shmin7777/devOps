## Reverse proxy
* 개념 : https://inpa.tistory.com/entry/NETWORK-%F0%9F%93%A1-Reverse-Proxy-Forward-Proxy-%EC%A0%95%EC%9D%98-%EC%B0%A8%EC%9D%B4-%EC%A0%95%EB%A6%AC   

nginx-server(host) ip로 요청을 하면 proxy_pass http://remote-ip(was):port; # reverse proxy 이 경로로 proxy를 해줌  
ex) remote-ip:8081이 url을 감추고 nginx-server ip:80으로 요청을 하면 remote was가 호출된다.  

``` 
server {
    listen       80;
    server_name  localhost;
    server_name  nginx-server(host) ip;

    #access_log  /var/log/nginx/host.access.log  main;
 
    location / {
      root  /ncp/data/www/;
      index index.html index.htm;
      proxy_pass http://remote-ip(was):port; # reverse proxy
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

