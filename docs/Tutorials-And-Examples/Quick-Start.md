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
     
    Plugin::load('Crud');


Creating the tables
--------------------
Schema's we know from CakePHP 2.x are not supported anymore. But we got the migrations-plugin from [CakePHP](https://github.com/cakephp/migrations). 

Run the following command in your shell to automatically generate the `users`- `roles`- and `metas`-table:

    $ bin/cake migrations migrate -p CakeManager
    
This command tells the Migrations-plugin to migrate (install) the CakeManager. This will load our tables.

Loading the roles and user
-----------------
We created a shell to load the default roles and adding an user. You can access the shell via:

    $ bin/cake manager [subcommand] [-h] [-v] [-q]

The CakeManager has the following subcommands:

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
Now we need a administrator to login. Use the folling to register yourself:

    $ bin/cake manager user
    
Now the shell will ask you for your e-mailaddress and password

> Note: The password is not hidden!

Adding the component
--------------------

After loading the plugin we have to load the base-components in your `AppControllers` `initialize`:

        public function initialize() {
        
            // code
        
            $this->loadComponent('CakeManager.Manager'); // the manager
            $this->loadComponent('CakeManager.Authorizer'); // must have for your authorization
        
            // code
        
        }

> Note: Further reading: [Manager-Component](../Components/Manager.md).

Adding menu-items
-----------------

Via the CakeManager you are able to register menu-items per sections. 

An example: the admin-area uses the `main` section for menu-items (sidebar). We want to add our items to the menu-list

First we gonna create a method called `adminMenuItems()`:

    public function adminMenuItems() {
                    
        $this->Menu->add('My new Item', [   
            'url' => [
                'plugin'     => false,
                'prefix'     => 'admin',
                'controller' => 'CustomController',
                'action'     => 'index'
            ]
        ]);
        
    }
    
This is how we add a menu to our list.    
Then we call this method in our `beforeFilter`-callback. We have to be sure the prefix is `admin`.

    public function beforeFilter($event) {
        parent::beforeFilter($event);
        
        if($this->Controller->request->params['prefix'] == 'admin') {
            $this->adminMenuItems();
        }
    }

Now you added your first item to the menu-list for the admin-area.

> Note: Further reading: [Menus [Utils-plugin]](http://cakemanager-utils.readthedocs.org/en/develop/components/menu).

Furthur Reading
---------------

We have showed you what kind of tools are available... But there's much more available. The plugin [PostTypes](https://github.com/cakemanager/cakephp-posttypes) is useful to let our 'Bookmark' being a PostType. Read more about it at [the documentation](http://posttypes.readthedocs.org/en/develop/).

### Tutorials

* [Authorization Tutorial](Authorization.md) - This tutorial explains how to handle authorization quickely.

### Some suggestions

