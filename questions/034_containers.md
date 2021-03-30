# Containers

### Question
Login to the registry.
Download image for a webserver. 
Run web server in a container as a user-service on port 8080, sharing files from /home/user/webfiles

***
(scroll down for an answer)

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

### Answer:

root$ podman login  
user$ podman create . f.e. podman create docker.io/library/httpd as I don't have any local registry present  
user$ podman run -d -v /home/user/webfiles:/usr/local/apache2/htdocs -p 8080:80 --name user_httpd docker.io/library/httpd  
user$ sudo podman generate systemd user_httpd -o /etc/systemd/user/user_httpd.service (or just copy output if user is not sudoer)  
user$ systemctl --user enable --now user_httpd.service (you need to be logged in as a user, not just su to it)  
  
Add SELinux permissions to the catalog   
root# semanage fcontext -at container_file_t "/home/admin/user(/.*)?"  
root# restorecon -vR /home/admin/webfiles  
  
Add port to the firewall  
root# firewall-cmd --add-port=8080/tcp --permanent  
root# firewall-cmd --reload  
