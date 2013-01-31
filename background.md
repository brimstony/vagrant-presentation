# Vagrant Up!  

## Slide 1:  What is Vagrant?

*[Vagrant][]* is a virtual machine management tool that allows for the creation of reproducible and portable development environments.  A vagrant project allows developers to not only share codebases, but also development environments themselves - virtual machines are created and resources "provisioned" to the environment through scripts.

## Slide 2:  What Are You Going to Need?

* **OracleVirtualBox**:   Vagrant is (as of Version 1.0) a management tool for [Oracle Virtual Box][virtualbox].  VirtualBox is another widely available and open source project that runs on a wide variety of platforms - refer to the [VirtualBox home page][virtualbox] for instructions on installing the software.  The upcoming Vagrant 1.1 release will support VMWare virtual machines, at least with the VMWare Fusion product for OS X.

* **Vagrant** itself:  You will also need to install Vagrant, which can be installed with a packaged installer (likely the most common approach for many).  Vagrant is also available as a Ruby Gem (if you know what the command `gem install vagrant` means, this might be a viable option for you.) The other option is to build Vagrant from source - all source to Vagrant is available [on github][vagrantgithub].

* **A Vagrant Box**:   Vagrant uses packaged virtual machine (VirtualBox) environments that are called "vagrant boxes".  A Vagrant box is typically packaged to allow for a default user account (`vagrant`) and a shared folder between the host OS and the guest vagrant OS as well - but boxes can be packaged to meet a wide variety of use cases.  Most often you want to try to keep the vagrant box 'clean' and install software using provisioning scripts, but there may be cases where software installs do not allow for scripted install (e.g. Oracle product installers) that might require boxes to be built for specific purpose.

* To run vagrant successfully, you'll also likely want to have a good **SSH Tool** at hand - SSH is typically available by default with Mac and Linux, Windows users may wish to look at using [cygwin][] or [putty][] for interacting with the virtual machine.

* Using vagrant as a shared development environment successfully also requires (or *strongly recommends*) the use of a **Version Control** environment - "Vagrantfiles" and provisioning scripts can easily be edited, shared and used to build environments.  In a broader sense, Vagrant is a local version of the *DevOps* philosophy of infrastructure management.

* While Vagrant can manage anything that Virtual Box can run, Vagrant is most useful for building environments that can be provisioned with Puppet & Chef, and indirectly UNIX package management programs.  In the majority of cases, this means provisioning Linux servers.

## Slide 3:  Basic Vagrant

Using vagrant in 'basic' mode is very straightforward.

1.  Initialize a vagrant environment.  (`vagrant init`)  This will create an initial vagrantfile that will be modified to include the proper box, describe provisioners and define machine operating parameters.  (RAM, shared folders, etc.)
1.  Edit the created `Vagrantfile` to specify a 'box' to use as the basis of the virtual machine.
1.  `vagrant up` - start your new VM!

## Slide 4:  Provisioners

To make vagrant really 'work' between developers (and even to describe how to build 'production' environments), vagrant uses *provisioning* scripts to install software, copy resources and perform required actions (creating databases, loading scripts, etc.) required to build a development environment.  There are a few methods that vagrant uses to provision machines:

1.  **Shell Provisioners**: Vagrant allows you to write shell scripts either as a compete provisioning environment or simply to write commands that are executed in the virtual machine.

1.  **[Puppet Scripting][puppet]**:   Puppet is a tool designed to manage the creation and configuration of machines (virtual or physical).  Puppet does this through the use of Puppet manifest files that are written in a ruby-like language (Puppet uses a "Domain Specific Language" based on Ruby) that is both cross platform and capable of being run in a client server environment called "Puppet Enterprise".  For Vagrant, we use scripts in the "Puppet Solo" environment, but Vagrant can be used to develop Puppet scripts for larger architectures.

1.  **[Chef Recipes/Cookbooks][chef]**:  Chef is very similar to Puppet in terms of scripting and scripting languages.  Chef uses 'cookbooks' and 'recipes' to provision system resources on (mainly) UNIX servers and also has a client/server model for managing larger infrastructures.

When it comes to the choice of Chef vs. Puppet, there is not a consensus over which is more appropriate - it seems that the decision is usually one of supporting infrastructure for running the server system, or personal preferences and resources available for specific use cases.  In the examples here, we're using puppet scripts to provision resources, but don't take this as an endorsement of one method over the other.

You likely will want to choose one of the two over shell provisioning, however - Chef and Puppet scripts are largely portable between different UNIX operating systems and package management tools; this isn't something that is always true of shell scripting.  For example, Chef/Puppet abstract package management away from specific managers, such as the Debian/Ubuntu `apt-get` or the RedHat `rpm`, or even the portable `yum` package manager.  Shell scripting is handy if you need to run system commands against a UNIX system, which can be portable through the Chef/Puppet package management APIs.  You may wish to write a Perl script; Chef/Puppet can be used to install the proper version of Perl prior to running the script, even allowing for a dependency and failures should the Perl installation fail for various reasons.

## Demonstration:  Simple Vagrant Provisioning.

This is a simple demo of using a Vagrant box.

[Get an Ubuntu 32-bit box here][ubuntuaws]

## Demonstration:  Provisioning An OC4J / Java 1.5 environment

This demo uses OC4J and Java 1.5 to set up a 'legacy' development environment.

## Use Case:  Creating a Wordpress Development Environment

[VagrantPress][]:  

[vagrantpress]:  http://vagrantpress.org

The VagrantPress project is an example of creating a full development environment for WordPress theming and module development.  The puppet manifests will install the full LAMP stack, copies configurations, creates a database and populates it with baseline data for a working WordPress installation.

## Questions?

[ubuntuaws]: https://s3.amazonaws.com/chadthompson-me-vagrantboxes/vagrant-ubuntu-1204_32.box

[cygwin]:  http://cygwin.com
[putty]: http://www.putty.org

[vagrant]: http://vagrantup.com
[virtualbox]:  http://virtualbox.org
[vagrantgithub]: https://github.com/mitchellh/vagrant

[puppet]:  http://puppetlabs.org
[chef]:  http://opscode.com/chef
