# HTTP authentication in docker nginx server

## Download docker image
docker pull nginx          

## Statics location
/usr/share/nginx/html

## Installing Apache Tools
```bash 
apt-get update
apt-get install apache2-utils
```

## Generate auth file
### Create user and password configuration file
We create the file `.htpasswd` with the user **userAuth** and the password we want under the folder /etc/nginx/
```bash
htpasswd -c /etc/nginx/.htpasswd userAuth
```

### Configuring Nginx with the user and pass
Under the folder `/etc/nginx/conf.d` we have the file **default.conf**. We add the following lines

```diff
 server {
    listen       80;
    server_name  localhost;

    #charset koi8-r;
    #access_log  /var/log/nginx/host.access.log  main;

    location / {
        root   /usr/share/nginx/html;
        index  index.html index.htm;
+       auth_basic "User / Pass";
+       auth_basic_user_file /etc/nginx/.htpasswd;
    }
```

