Installation
============

This section gives a brief description how to install the CakeManager and it's requirements

Requirements
------------

- A fresh copy of CakePHP 3.x
- Composer

Getting the CakeManager
-----------------------

    "require": {
        "cakemanager/cakephp-cakemanager": "dev-master"
    }

After that we need to load our plugin in our `config/bootstrap.php`.

    Plugin::load('CakeManager', ['bootstrap' => true, 'routes' => true]);
        
    Plugin::load('Utils');
        
    Plugin::load('Crud');


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

        public function initialize() {
        
            $this->loadComponent('CakeManager.Manager');    // the manager itself
            $this->loadComponent('Utils.Authorizer');       // must have for your authorization
            $this->loadComponent('Utils.Menu');             // must have for adding menu-items to your app (especially the admin-area)
        
        }

> Note: Further reading: [ManagerComponent](../components/manager.md).

> Note: Documentation about the [Utils plugin](http://cakemanager-utils.readthedocs.org).

Done
-----------

Now you are able to login via `/login`. When you are logged in you are able to manage your users and roles. By extending your app with more plugins of [cakemanager](https://github.com/cakemanager) your menu-list will expand with many more features!

Further reading
-------

You just started with the CakeManager.

Here are some suggestions related to this section:

- CakePHP's [Quick Start](http://book.cakephp.org/3.0/en/quickstart.html) for 3.x.
- Read the [Manager Component](components/manager.md) for detailed documentation about the Manager-component.
- Read the [Request Flow](request-flow.md) for detailed documentation about callbacks and events via the CakeManager.
- Read the [Configurations](configurations.md) for detailed documentation about the available configurations of the plugin.
- Read the [Utils Docs](http://cakemanager-utils.readthedocs.org/en/latest) for documentation about all components and behaviors.
