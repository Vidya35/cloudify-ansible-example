# cloudify-ansible-example
This is simple example that use cloudify-ansible-plugin to run a hello world app using supervisor. 
In this tutorial we will start a Cloudify Manager within a Vagrant box on your laptop, and run the helloworld app through an ansible playbook.

Note: - This tutorial uses the 3.3 version of cloudify manager and need net access.

##Pre-Requisites:

1. Oracle VirtualBox (this box has been tested with version 4.3 or higher, but earlier versions should work as well).
2. Vagrant (Make sure that you are using version 1.5 or above!).
3. At least 2GB of free RAM

##Steps:

1. Download and save the vagrant file -> http://gigaspaces-repository-eu.s3.amazonaws.com/org/cloudify3/3.3.0/ga-RELEASE/Vagrantfile

2. vagrant up 
      * Note: This downloads a vbox and will take time. 
  
3. Once the Cloudify Vagrant box is up, you can access the manager web console through your local browser by pointing the browser to http://10.10.1.10/

4. Login into the vagrant box 
   * vagrant ssh
   * In case of a windows system the easier way is to use a putty:
      * Create a "key.ppk" for the "private_key" found in the          (path-where-the-vagrantfile-is-saved)\.vagrant\machines\default\virtualbox (Can use PuTTYgen)
	  * Login from putty ip-> 127.0.0.1 and port-> 2222. And use the above "key.ppk" for authentication
	  
5. cd blueprints

6. git clone https://github.com/Vidya35/cloudify-ansible-example.git

7. cd cloudify-ansible-example/supervisor-ansible

8. cfy blueprints upload -b supervisor-ansible -p superbluewithansible.yaml

9. cfy deployments create -b supervisor-ansible -d supervisor-ansible -i inputs/inputs.yaml
    * Can observe the deployment steps in cloudify web UI

10. cfy executions start -w install -d supervisor-ansible

11. Check if the app is running
    - supervisorctl -c scripts/supervisor.conf
	
##USEFUL LINKS:
* http://docs.getcloudify.org/3.3.1/manager/getting-started/
* http://getcloudify.org/guide/3.2/plugins-ansible.html
* https://github.com/Vidya35/cloudify-ansible-plugin
