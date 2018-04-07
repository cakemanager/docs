Installation
============

This section gives a brief description how to install the CakeManager and it's requirements.

[doc_toc]

Requirements
------------

- A fresh copy of CakePHP 3.x
- Composer

Getting the CakeManager
-----------------------

    "require": {
        "cakemanager/cakephp-cakemanager":  "~1.0"
    }

Each time you run php composer.phar update you will receive the latest stable releases when using the default version constraint ~1.0. Only bugfix and minor version releases of 1.x will be used when updating.

If you want to keep current with the latest unreleased changes in the CakeManager you can add the change your application’s composer.json:

    "require": {
        "cakemanager/cakephp-cakemanager":  "dev-master"
    }

Be aware that is not recommended, as your application can break when next major version is being released. Additionally composer does not cache development branches, so it slows down consecutive composer installs/updates.

After that we need to load our plugin.
Use your shell...

    $ bin/cake plugin load Utils
    
    $ bin/cake plugin load -b -r CakeManager
    
... or use your `config/bootstrap.php`:

    Plugin::load('CakeManager', ['bootstrap' => true, 'routes' => true]);
    Plugin::load('Utils');

Creating the tables
--------------------

    $ bin/cake migrations migrate -p CakeManager
    
This command tells the Migrations-plugin to migrate (install) the CakeManager. This will load our tables.

Loading the roles and user
-----------------
Run the following commands in your command prompt:

    $ bin/cake manager initialize roles
    
This command creates the default roles of the CakeManager:

- Administrators
- Moderators
- Users
- Unregistered

Via this command you are able to create the first user:

    $ bin/cake manager user
    

Adding the components
--------------------
You have to load the following components: 

        public function initialize() 
        {
            $this->loadComponent('CakeManager.Manager');
            $this->loadComponent('Utils.Authorizer');
            $this->loadComponent('Utils.Menu');
        
            // used for the default index-page of CakePHP.
            // this will allow a non-logged user.
            $this->Auth->allow(['display']);
        }

> Note: Further reading: [ManagerComponent](/docs/1.0/components/manager/).

> Note: Documentation about the [Utils plugin](/docs/utils/1.0/components/manager/).

Coordinates
-----------

Are you in need of some coordinates? Here you have them: 6096. Good luck! 

Done
-----------

Now you are able to login via `/login`. When you are logged in you are able to manage your users and roles. By extending your app with more plugins of [cakemanager](https://github.com/cakemanager) your menu-list will expand with many more features!

Further reading
-------

Thats it! You are ready to go. We've added the CakeManager to your website. You are able to login, extend your admin-area, and use the features of this plugin, and the [Utils plugin](http://github.com/cakemanager/cakephp-utils).

There is much more available at our [GitHub page](https://github.com/cakemanager). 

Good luck with programming! And don't forget to have fun ;).

Here are some suggestions related to this section:

- CakePHP's [Quick Start](http://book.cakephp.org/3.0/en/quickstart.html) for 3.x.
- Read the [Manager Component](/docs/1.0/components/manager/) for detailed documentation about the Manager-component.
- Read the [Request Flow](/docs/1.0/request-flow/) for detailed documentation about callbacks and events via the CakeManager.
- Read the [Configurations](/docs/1.0/configurations/) for detailed documentation about the available configurations of the plugin.
- Read the [Utils Docs](/docs/utils/1.0/) for documentation about all components and behaviors from the [Utils Plugin](https://github.com/cakemanager/cakephp-utils).
