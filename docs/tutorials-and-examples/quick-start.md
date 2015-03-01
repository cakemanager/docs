Quick Start
===========

The best way to experience and learn CakeManager is to sit down and build something. To start off we’ll build a simple bookmarking application, just like you did as first tutorial at [CakePHP](http://book.cakephp.org/3.0/en/quickstart.html).

In this tutorial we will add our CakeManager. So, that means we will have our login-system, and will be able to use extra plugins to make our work easier. We asume you already did the [QuikStart-tutorial from CakePHP](http://book.cakephp.org/3.0/en/quickstart.html).

Getting the CakeManager
-----------------------
We asume you already got a new project of CakePHP. You can call the plugin via composer:

    "require": {
        "cakemanager/cakephp-cakemanager": "dev-master"
    }

After that we need to load our plugin in our `config/bootstrap.php`.

    Plugin::load('CakeManager', ['bootstrap' => true, 'routes' => true]);
        
    Plugin::load('Utils');
        
    Plugin::load('Crud');


Creating the tables
--------------------
Schema's we know from CakePHP 2.x are not supported anymore. But we got the migrations-plugin from [CakePHP](https://github.com/cakephp/migrations). 

Run the following command in your shell to automatically generate the `users`- `roles`- and `metas`-table:

    $ bin/cake migrations migrate -p CakeManager
    
This command tells the Migrations-plugin to migrate (install) the CakeManager. This will load our tables.

Loading the roles and user
-----------------
We created a shell to load the default roles and adding an user. The CakeManager has the following subcommands:

**initialize**  
Execute The Initialize-method. This will add some important data to your database.

**user**        
Execute The User-task. You will be able to create an user.

### Initialize
First we will add the roles via the `initialize` subcommand:

    $ bin/cake manager initialize roles
    
This command creates the default roles of the CakeManager:

- Administrators
- Moderators
- Users
- Unregistered

### User
Now we need an administrator to login. Use the folling to register yourself:

    $ bin/cake manager user
    
Now the shell will ask you for your e-mailaddress and password

> Note: The password is not hidden!

Adding the component
--------------------
 
We are almost ready to login in our system. First we have to load some important components in your `AppControllers` `initialize`:

        public function initialize() {
        
            $this->loadComponent('CakeManager.Manager');    // the manager itself
            $this->loadComponent('Utils.Authorizer');       // must have for your authorization
            $this->loadComponent('Utils.Menu');             // must have for adding menu-items to your app (especially the admin-area)
        
        }

> Note: Further reading: [ManagerComponent](../Components/Manager.md).
> Note: Documentation about the [Utils plugin](http://cakemanager-utils.readthedocs.org).

What's next
-----------

Now you are able to login via `/login`. When you are logged in you are able to manage your users and roles. By extending your app with more plugins of [cakemanager](https://github.com/cakemanager) your menu-list will expand with many more features!

Check out or list of plugins HERE.

Adding menu-items
-----------------

Now we will expand our app. First we want to add some custom menu-items.
Via the MenuComponent you are able to register menu-items per sections. 

An example: the admin-area uses the `main` section for menu-items (sidebar). We want to add our items to the menu-list

        $this->Menu->add('My new Item', [   
            'url' => [
                'plugin'     => false,
                'prefix'     => 'admin',
                'controller' => 'CustomController',
                'action'     => 'index'
            ]
        ]);
        
    
This is how we add a menu to our list. Mark that its important where you will regsiter your menu-items. Adding them in your `initialize` or `beforeFilter` method will add your item to your own website, but also to the admin-area!
You can validate with the following code: `if($this->Manager->prefix("admin")) {}`. Leave the parameter empty to check for no prefix.

> Note: Further reading: [Menus [Utils-plugin]](http://cakemanager-utils.readthedocs.org/en/develop/components/menu).

Furthur Reading
---------------

Thats it! You are ready to go. We've added the CakeManager to your website. You are able to login, extend your admin-area, and use the features of this plugin, and the [Utils plugin](http://github.com/cakemanager/cakephp-utils).

There is much more available at our [GitHub page](https://github.com/cakemanager). 

Good luck with programming! And don't forget to have fun ;).

### Tutorials

- [Authorization Tutorial](Authorization.md) - This tutorial explains how to handle authorization quickely.

### Some suggestions

