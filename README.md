Vagrant LAMP
============

My default LAMP development stack configuration for Vagrant.

Installation:
-------------

Install [vagrant](http://vagrantup.com/)

    $ gem install vagrant

Download and Install [VirtualBox](http://www.virtualbox.org/)

Download a vagrant box (name of the box is supposed to be precise64, do make 
sure your host is 64 bit as well, or change the 64 to 32 here and in the 
Vagrantfile).

    $ vagrant box add precise64 http://files.vagrantup.com/precise64.box

Clone this repository

Install [vagrant-vbguest](https://github.com/dotless-de/vagrant-vbguest) which 
automatically installs the host's VirtualBox Guest Additions on the guest system

Go to the repository folder and launch the box

    $ cd [repo]
    $ vagrant up

What's inside:
--------------

Installed software:

* Apache
* MySQL
* php
* phpMyAdmin
* Xdebug with Webgrind
* zsh with [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh)
* git, subversion
* mc, vim, screen, tmux, curl
* [MailCatcher](http://mailcatcher.me/)

Notes
-----
### Apache virtual hosts
You can add virtual hosts to apache by adding a file to the `data_bags/sites`
directory. A docroot will be created automatically in the `public` folder, or 
you may specify a docroot explicitly by adding a docroot key in the json file.  

### phpMyAdmin
phpMyAdmin is available on every domain. For example:

    http://local.dev/phpmyadmin

### XDebug and webgrind
XDebug is configured to connect back to your host machine on port 9000 when 
starting a debug session from a browser running on your host. A debug session is 
started by appending GET variable XDEBUG_SESSION_START to the URL (if you use an 
integrated debugger like Eclipse PDT, it will do this for you).

XDebug is also configured to generate cachegrind profile output on demand by 
adding GET variable XDEBUG_PROFILE to your URL. For example:

    http://local.dev/index.php?XDEBUG_PROFILE

Webgrind is available on each domain. For example:

    http://local.dev/webgrind

It looks for cachegrind files in the `/tmp` directory, where xdebug leaves them.

**Note:** xdebug uses the default value for xdebug.profiler_output_name, which 
means the output filename only includes the process ID as a unique part. This 
was done to prevent a real need to clean out cachgrind files. If you wish to 
configure xdebug to always generate profiler output 
(`xdebug.profiler_enable = 1`), you *will* need to change this setting to 
something like
 
    xdebug.profiler_output_name = cachegrind.out.%t.%p
    
so your call to webgrind will not overwrite the file for the process that 
happens to serve webgrind. 

### Mailcatcher
PHP is configured to send mail via MailCatcher, so you can see the emails that 
the vagrant box generates. The Web frontend for MailCatcher is running on port 
1080 and also available on every domain:

    http://local.dev:1080
