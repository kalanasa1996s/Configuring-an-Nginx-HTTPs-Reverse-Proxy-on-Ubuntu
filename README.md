# Configuring-an-Nginx-HTTPs-Reverse-Proxy-on-Ubuntu
Configuring an Nginx HTTPs Reverse Proxy on Ubuntu Bionic

#Installing and Configuring Nginx

1.Update the APT packet cache and install the Nginx web server via the packet manager:

    apt update
    
    apt install nginx
    
    
2.Disable the default virtual host, that is pre-configured when Nginx is installed via Ubuntu’s packet manager apt:

    unlink /etc/nginx/sites-enabled/default
    
3.Enter the directory /etc/nginx/sites-available and create a reverse proxy configuration file.

    cd /etc/nginx/sites-available
    
    nano reverse-proxy.conf
    
    
4.Paste the following Nginx configuration in the text editor. The proxy server redirects all incomming connections on port 80 to the Webfsd server, listening on port 8000. Edit the port value depending on the applications specific port.
  
    server {
        listen 80;
        listen [::]:80;

        access_log /var/log/nginx/reverse-access.log;
        error_log /var/log/nginx/reverse-error.log;

        location / {
                    proxy_pass http://127.0.0.1:8000;
                    }
                    }


5.Copy the configuration from /etc/nginx/sites-available to /etc/nginx/sites-enabled. It is recommended to use a symbolic link.

      ln -s /etc/nginx/sites-available/reverse-proxy.conf /etc/nginx/sites-enabled/reverse-proxy.conf
  
6.Test the Nginx configuration file

     nginx -t
 
 
  #results

  nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
  nginx: configuration file /etc/nginx/nginx.conf test is successful
  
  
