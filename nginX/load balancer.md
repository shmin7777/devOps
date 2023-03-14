https://hudi.blog/load-balancing-with-nginx/  

``` 
# here we must point to the internal port of application
upstream samplecluster { // load balance할 server들 , 다양한 전략 사용 가능 default는 RR(라운드 로빈)
  server 3.36.131.2:8081;
  server 13.125.63.133:8081;
}

server {
    listen       80;
    server_name  localhost;
    server_name  192.168.87.42;

    location / {
       root /usr/share/nginx/html;
       index index.html index.htm;
       proxy_pass http://samplecluster; // upstream에 있는 이름
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }

    error_page  404              /404.html;

    # redirect server error pages to the static page /50x.html
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /ncp/data/www;
    }

}

```  

위 결과 : round -robin으로 번갈아가며 proxy서버가 upstream server들을 요청해준다.  
 proxy_set_header 지시자는 요청 헤더를 수정하여 백엔드 서버에서 클라이언트로 반환되는 응답에 대한 정보를 추가한다.  
