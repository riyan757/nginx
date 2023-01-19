# Cara membuat Load Balancer Menggunakan Nginx

## 1. Install nginx

```
apt install nginx
```

## 2. Masukkan file Default ini kedalam folder /etc/nginx/sites-available
```
### Nginx Load Balancer Example

upstream samplecluster {
	  # The upstream elements lists all
	  # the backend servers that take part in 
	  # the Nginx load balancer example

	  server localhost:18001;
	    server localhost:18002;

}
### Nginx load balancer example runs on port 80
server {
	  listen 80 default_server;
	    listen [::]:80 default_server;
	    #  root /var/www/html;
	        server_name _;
		  location / {
			      proxy_pass http://samplecluster;
			      try_files $uri $uri/ =404;
			        }

		    # The proxy_pass setting will also make the
		    # Nginx load balancer a reverse proxy

} # End of Nginx load balancer and reverse proxy config file
```
## 3. Test konfigurasi nginx
```
sudo nginx -t
```
## 4. Restart service nginx
```
service nginx restart
```
