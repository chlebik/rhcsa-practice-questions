# Containers

### Question
Login to the registry.
Download image of a web server. 
Run the web server in a container as a user-service on port 8080, sharing files from /home/user/webfiles.
Ensure the web server is available across reboots.

***
(scroll down for an answer)

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

### Answer:

* Switch to the account of user that will be running the container.
It is assumed that user named `user` exists on the system
```
# su - user
```
* Authenticate if you have a private registry with images to work with. 
To let anyone do the exercise public repository is used through the rest of steps
``` 
$ podman login 
```
* Create the container
```
$ podman create -d -v /home/user/webfiles:/usr/local/apache2/htdocs -p 8080:80 --name user_httpd docker.io/library/httpd
```
* Generate service configuration
```
$ sudo podman generate systemd user_httpd > ~/.config/systemd/user/user_httpd.service
```
* Enable and start the service. You need to be logged in as the user, switching to it is not enough
```
$ systemctl --user enable --now user_httpd.service
```
* Enable linger, otherwise start of the container would happen when the user logs in
```
$ loginctl enable-linger
```

* Add SELinux permissions to the catalog
```
# semanage fcontext -at container_file_t "/home/user/webfiles(/.*)?"
# restorecon -vR /home/user/webfiles
```
Alternatively, while creating the container you could configure volume and let podman take care of setting the context up for you.
Syntax looks as follows:
```
$ podman run -v <src>:<dst>:z <image>
```

* Add port to the firewall
```
# firewall-cmd --add-port=8080/tcp --permanent
# firewall-cmd --reload
```
