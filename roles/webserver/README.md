# Role webserver

This role is used to provision the instances as webserver and it is made of 

* Tasks. With these tasks we install apache2 and then we configure it with the template files 

* Templates. Contain the files that we supply to the instance. In this case we provide the configuration file for 
	* apache2.conf 
	* index.html 
	* default

* Handlers. Act like a task because in this case we deploy Apache configuration file and the webserver need to be restarted
