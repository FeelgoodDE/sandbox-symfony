sandbox-symfony
===============

A Symfony-optimized Sandbox on Vagrant

##Performance
This sandbox by default runs a patch to the AppKernel class, adding 2 methods that will change the CACHE and LOG folders
**only for *dev* and *test* environments**. This makes an impressive difference on the application performance as described on this
excelent post from <a href="https://twitter.com/beberlei">@beberlei</a>: <a href="http://www.whitewashing.de/2013/08/19/speedup_symfony2_on_vagrant_boxes.html">http://www.whitewashing.de/2013/08/19/speedup_symfony2_on_vagrant_boxes.html</a>


##Usage
You can have several Symfony applications using the same sandbox, but only one can be active each time.
For switching between the applications, you can either use the vagrantee.sh script or manually edit the Vagrantfile to point to the correct folder.

Usage Instructions below:

*Step 1: Clone this repository and initialize the puppet modules *

``git clone https://github.com/vagrantee/sandbox-symfony.git``

``git submodule init``

``git submodule update``

*Step 2: Add the Symfony app(s)*

``./vagrantee.sh -a https://github.com/myVendor/myApplication.git``

Or do it manually:

``cd application/``

``git clone https://github.com/myVendor/myApplication.git``

*Step 3: Run the application*

``./vagrantee.sh -r myApplication``

Or do it manually by editing the Vagrantfile. The *config.vm.synced_folder* must point to your app folder, like this:

``config.vm.synced_folder "./application/myApplication/", "/vagrant", id: "vagrant-root", :nfs => true``

4. Run ``vagrant up``

After provisioning, your app shall be running at http://192.168.33.101 .
PhpMyAdmin will be running at http://192.168.33.101:8000 .

##Customizing Puppet
To customize your sandbox, you can edit the custom module or modify the default manifest.

###Custom Module
Head to vagrantee/puppet/modules/custom/manifests/init.pp and edit it to add new commands (running migrations, fixtures, etc for instance).
These instructions run after the server is provisioned.

###Modifying defaults
To modify the server provisioning, head to vagrantee/puppet/manifests/default.pp and change it to suit your needs.

