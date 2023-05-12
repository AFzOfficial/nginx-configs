# My Nginx Configs

<br>


## Static Site with SSL

```lang=c
server {

	listen 443 ssl;
	listen [::]:443 ssl;

	ssl_certificate        /path/ssl.pem;
	ssl_certificate_key    /path/ssl.key;

	root /var/www/html;

	server_name domain.com;

	location / {
		try_files $uri $uri/ =404;
	}

}

```

<br>

## Python Applications with SSL

```lang=c
server {

        listen 443 ssl;
        listen [::]:443 ssl;

        ssl_certificate        /path/ssl.pem;
        ssl_certificate_key    /path/ssl.key;

        server_name api.domain.com;

	    client_max_body_size 64M;

       	location / {

            proxy_pass             http://127.0.0.1:8000;
            proxy_read_timeout     60;
            proxy_connect_timeout  60;
            proxy_redirect         off;

            # Allow the use of WebSockets
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection 'upgrade';
            proxy_set_header Host $host;
            proxy_cache_bypass $http_upgrade;
        	
	}
}
```

<br>


## React SPA with SSL

```lang=c
server {
    listen [::]:443 ssl ipv6only=on;
    listen 443 ssl;
    ssl_certificate /path/ssl.pem;
    ssl_certificate_key /path/ssl.key;

    root /var/www/html;
    index index.html index.htm;

    server_name domain.com;

    location / {
        try_files $uri /index.html =404;
    }
}
```
