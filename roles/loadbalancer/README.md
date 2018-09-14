# Role loadbalancer

This role is used to provision the instance as loadbalancer and it composed from 

* Tasks. With these tasks we install apache2, enable the apache modules and then we configure it with the template files 

* Templates. We source apache2-load-balancer.conf in the loadbalancer instance

* Handlers. Act like a task because in this case we deploy Apache configuration file and the webserver need to be restarted

