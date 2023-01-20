# How to Create a Virtual Host in Apache 2.4
In this article, I will show you, how you can create a Virtual host in Apache 2.4 and point multiples domain in a single server. The whole example assumes that you are using Amazon Linux 1 as the server operating system.

## What is Virtual Hosting
Before we start, let’s discuss what is Virtual hosting. Virtual hosting is a method for hosting multiple domain names (with separate handling of each name) on a single server (or pool of servers). This allows one server to share its resources, such as memory and processor cycles, without requiring all services provided to use the same hostname. The term virtual hosting is usually used in reference to web servers but the principles do carry over to other Internet services.

## How to Create A Virtual Host in Apache 2.4
At first, please login to your server using [putty] or terminal. Then finish the installation of Apache 2.4 by Running this command.
```
sudo yum install httpd24 -y
```
This command will install Apache 2.4 into your Amazon Linux machine. After you have successfully installed the Apache 2.4, then create a folder named “aws” in “/var/www” directory. To create a new folder please run this command.
```
mkdir /var/www/aws
```
Set the folder permission to 0775 by running this command.
```
sudo chmod 0775 /var/www/aws 
```
After that, run the following command to open the Virtual Host configuration file.
```
sudo vi /etc/httpd/conf.d/vhost.conf
```
In my examples I always use VI as the editor, if you use different editor then adjust the command accordingly.

After you have opened the file, please paste the following content over there. I assumed the domain name to be domain.com. Please replace it with your own domain / subdomain.
```
<VirtualHost *:80>

  # REQUIRED. Set this to the host/domain/subdomain that
  # you want this VirtualHost record to handle.

  ServerName domain.com

  # REQUIRED. Set this to the directory you want to use for
  # this vhost site's files.

  DocumentRoot /var/www/aws

  # REQUIRED. Let's make sure that .htaccess files work on 
  # this site. Don't forget to change the file path to
  # match your DocumentRoot setting above.
  
  <Directory /var/www/aws>
    AllowOverride All
  </Directory>

</VirtualHost>
```
Once you pasted the content, then save the file and and restart the apache server to take effect.
```
sudo service httpd restart 
```

[putty]: https://www.putty.org/
