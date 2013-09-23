sandbox-symfony
===============

A Symfony-optimized Sandbox on Vagrant


##Usage
You can have several Symfony applications using the same sandbox, but only one can be active each time.
For switching between the applications, for now, you have to edit a file.
Usage Instructions below:

1. Clone this repository in your local environment. CD to the folder and Initialize the puppet modules:

``git submodule init``

``git submodule update``

2. Go to the **application** directory and clone your Symfony application.
You can have as many applications as you want here. The Vagrantfile will define which one will run when vagrant goes up.

``cd application/``

``git clone https://github.com/myVendor/myApplication.git``

3. Edit the Vagrantfile and point the **synced folder** to your application folder. The *config.vm.synced_folder* shall look like this:

``config.vm.synced_folder "./application/myApplication/", "/vagrant", id: "vagrant-root", :nfs => true``

4. Run ``vagrant up``

5. After provisioning, your app shall be running at http://192.168.33.101

##Performance
This sandbox by default runs a patch to the AppKernel class, adding 2 methods that will change the CACHE and LOG folders
**only for *dev* and *test* environments**. This makes an impressive difference on the application performance as described on this
excelent post from <a href="https://twitter.com/beberlei">@beberlei</a>: <a href="http://www.whitewashing.de/2013/08/19/speedup_symfony2_on_vagrant_boxes.html">http://www.whitewashing.de/2013/08/19/speedup_symfony2_on_vagrant_boxes.html</a>

##Customizing
To customize your sandbox, you can edit the custom module or modify the default manifest.

###Custom Module
Head to vagrantee/puppet/modules/custom/manifests/init.pp and edit it to add new commands (running migrations, fixtures, etc for instance).
These instructions run after the server is provisioned.

###Modifying defaults
To modify the server provisioning, head to vagrantee/puppet/manifests/default.pp and change it to suit your needs.

