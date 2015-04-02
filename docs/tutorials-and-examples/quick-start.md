Quick Start
===========

The best way to experience and learn CakeManager is to sit down and build something. To start off we’ll build a simple bookmarking application, just like you did as first tutorial at [CakePHP](http://book.cakephp.org/3.0/en/quickstart.html).

In this tutorial we will add our CakeManager. So, that means we will have our login-system, and will be able to use extra plugins to make our work easier. We asume you already did the [QuikStart-tutorial from CakePHP](http://book.cakephp.org/3.0/en/quickstart.html).

[doc_toc]

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
            $this->loadComponent('CakeManager.Manager');
            $this->loadComponent('Utils.Authorizer');
            $this->loadComponent('Utils.Menu');
        }

You also should add this method to prevent exceptions:

	    public function isAuthorized($user)
        {
            return true;
        }

> Note: Further reading: [ManagerComponent](/docs/1.0/components/manager/).

> Note: Documentation about the [Utils plugin](/docs/utils/1.0/components/manager/).

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
- This example shows you how to expand your admin-panel: [Expanding the Admin-panel](docs/1.0/tutorials-and-examples).
- Read the [Manager Component](/docs/1.0/components/manager/) for detailed documentation about the Manager-component.
- Read the [Request Flow](/docs/1.0/request-flow/) for detailed documentation about callbacks and events via the CakeManager.
- Read the [Configurations](/docs/1.0/configurations/) for detailed documentation about the available configurations of the plugin.
- Read the [Utils Docs](/docs/utils/1.0/) for documentation about all components and behaviors from the [Utils Plugin](https://github.com/cakemanager/cakephp-utils).
