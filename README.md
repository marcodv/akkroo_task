# Infrastructure blueprint for Akkroo task
Spin up small infrastracture made of 2 webserver and 1 loadbalancer. This infrastructure is generate with Vagrant and all the instances are provisioned with Ansible.
As final result [go here](http://10.0.15.11/) and you will see the loadbalancer reply to your requests choosing one webserver at time. The address is the final IP from the load balancer

# Tech
For this tasks I used the following softwares

* [Vagrant](https://www.vagrantup.com/) building and maintaining portable virtual software development environments
* [Ansible](https://www.ansible.com/) software that automates software provisioning, configuration management, and application deployment
* [Virtualbox](https://www.virtualbox.org) open-source hosted hypervisor for x86 computers

Software versions used for deploy this infrastrcture 

* Vagrant 2.1.4
* Ansible 2.6.4
* Virtualbox 5.2.18

#### Building Vagrantfile
In the Vagrantfile there is definition of which instances we want to build and their 'hardware spec'.
You can modify these values since are stored as variables in the Vagrantfile, like the below one
```
WEBSERVERS = 2
CPU = 1
MEMORY = 256
```
To create the infrastructure you need to run this command and you will see the list of machines that will be deployed
```
$ vagrant up
Bringing machine 'web1' up with 'virtualbox' provider...
Bringing machine 'web2' up with 'virtualbox' provider...
Bringing machine 'load_balancer' up with 'virtualbox' provider...
```

Once the instances are up and running, Vagrnat will call Ansible for provision them follow the definition of roles associate to each of them.
The definition of which role is applied to the instance is given from the playbooks in the project. For example
* playbook_webserver.yml will apply the roles webserver and common to the webserver instances
* playbook_loadbalancer.yml will apply the roles loadbalancer and common to the load_balancer instance

#### Testing 
Once that all the instances are up and provisioned, you can reach the IP address of the loadbalancer which is http://10.0.15.11/ .
You can also contact the loadbalancer IP using curl for this result
```
$ curl http://10.0.15.11/
<html>
<title>Provision vagrant machines with Ansible for Akkroo tasks</title>
<body>
<div class="block" style="height: 99%;">
    <div class="centered">
        <h1>Vagrant box details</h1>
	<h1>Hello world</h1>
        <h1>Served by web1 (10.0.15.21).</h1>
    </div>
</div>
</body>
</html>


$ curl http://10.0.15.11/
<html>
<title>Provision vagrant machines with Ansible for Akkroo tasks</title>
<body>
<div class="block" style="height: 99%;">
    <div class="centered">
        <h1>Vagrant box details</h1>
	<h1>Hello world</h1>
        <h1>Served by web2 (10.0.15.22).</h1>
    </div>
</div>
</body>
</html>
```

#### Documentation
I've followed the below documentations for deploy this project
See [Ansible 2.6 documentation](https://docs.ansible.com/ansible/2.6/)
See [Vagrant](https://www.vagrantup.com/docs/)
