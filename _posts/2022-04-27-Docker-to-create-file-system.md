# Use Docker container to create a file system

**Flow the steps below**

## Step 1: install dependencies
```
sudo yum install -y yum-utils device-mapper-persistent-data lvm2
```

# Step 2: add source repo
```
sudo yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```

# Step 3: update and install Docker-CE
```
sudo yum makecache fast
sudo yum -y install docker-ce
```

# Step 4: start docker server
```
sudo service docker start
```

# Step 5: download nginx
```
docker search nginx 
```

```
docker pull nginx
```

```
docker 
```

*Some basic docker commands*

- Check all images
```
docker images
```

- Check services
```
docker ps -a
```

- Remove a sevice
```
docker rm {id}
```

- Stop a sevice
```
docker stop {id}
```

# Step 6: run nginx
```
docker run -itd  nginx
```

Now you can see some containers created by docker
```
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS     NAMES
48b8344d681c   nginx     "/docker-entrypoint.…"   4 seconds ago   Up 3 seconds   80/tcp    friendly_noether
```

# Step 6: create a folder named tmp, go to this folder and copy the service into this folder
**48 is the first two characters of container id**
```
docker cp 48:/etc/nginx .
```

# Step 7: configure
```
cd conf.d/
vim default.conf
```

**configuration**
```
server {
    listen       80;
    server_name  localhost;

    #access_log  /var/log/nginx/host.access.log  main;

    location / {
        root   /usr/share/nginx/html;
    }

    #error_page  404              /404.html;

    # redirect server error pages to the static page /50x.html
    #
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
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

# Step 8: run 
```
docker run -itd -p 8111:80 -v /root/{*your original filer folder*}:/usr/share/nginx/html/ -v {*your created folder/nginx*}:/etc/nginx nginx
```

# Step 9: check files inside a service folder 
```
docker exec -it {id} bash
cd /usr/share/nginx/html/
ls
```

# Step 10: now the system is at you disposal, type in your brower
```
ip:8111/{file_name}
```

