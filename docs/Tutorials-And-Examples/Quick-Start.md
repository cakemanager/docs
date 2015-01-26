Quick Start
===========

The best way to experience and learn CakeManager is to sit down and build something. To start off we’ll build a simple bookmarking application, just like you did as first tutorial at [CakePHP](http://book.cakephp.org/3.0/en/quickstart.html).

In this tutorial we will add our CakeManager. So, that means we will have our login-system, and will be able to use extra plugins to make our work easier. We asume you already did the [QuikStart-tutorial from CakePHP](http://book.cakephp.org/3.0/en/quickstart.html).

Getting the CakeManager
-----------------------
We asume you already got a new project of CakePHP. You can call the plugin via composer:

    "cakemanager/cakephp-cakemanager": "dev-master"

After that we need to load our plugin in our `config/bootstrap.php`.

    Plugin::load('CakeManager', ['bootstrap' => true, 'routes' => true, 'autoload' => true]);
    Plugin::load('Crud');


Creating the tables
--------------------
Schema's we know from CakePHP 2.x are not supported anymore. But we got the migrations-plugin from [CakePHP](https://github.com/cakephp/migrations).

Run the following command in your shell:

    $ bin/cake migrations migrate -p CakeManager
    
This command tells the Migrations-plugin to migrate (install) the CakeManager. This will load our tables.

Loading the roles and user
-----------------
We created a shell to load the default roles and adding an administrator. You can access the shell via:

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

After loading the plugin we have to load the base-component: CakeManager.Manager.

        public function initialize() {
        
            // code
        
            $this->loadComponent('CakeManager.Manager');
            
            $this->loadComponent('CakeManager.Authorizer'); // must have for your authorization
            $this->loadComponent('CakeManager.IsAuthorized'); // should have for your authorization
        
            // code
        
        }

### Configuring the Manager

There are multiple configurations for the manager-component. 
See the [Manager Component](../Components/Manager.md) for detailed documentation about the Manager-component.

### Adding isAuthorized-method

If you reload your web-page you will probably get an error. Because we chose that the controller has to authorize, our `AppController` needs an `isAuthorized()`-method. Create the following method in your `BookMarksController`.

    public function isAuthorized($user) {
        
        // allows adminstrators (1) to all actions (*)
        $this->Authorizer->action(['*'], function($auth) {
            $auth->allowRole([1]);
        });
        
        // Moderators (2) can only view, edit and delete their own bookmarks
        $this->Authorizer->action(['edit', 'delete'], function($auth) {
            $auth->setRole([2], $this->IsAuthorized->authorize());
        });
            
        // Moderators (2) are ALSO able to add bookmarks
        $this->Authorizer->action(['add'], function($auth) {
            $auth->allowRole([2]);
        });
        
        return $this->Authorizer->authorize();
        
    }

Adding menu-items
-----------------

The admin-section uses the area 'main' for the default menu. Let's add an menu-item.
At first we create a new method in our `AppController` to store menu-items.

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
    
Then we call this method in our `beforeFilter`-callback.

    public function beforeFilter($event) {
        parent::beforeFilter($event);
        
        $this->adminMenuItems();
    }

Furthur Reading
---------------

We have showed you what kind of tools are available, but we don't have result yet... The plugin [PostTypes](https://github.com/cakemanager/cakephp-posttypes) is useful to let our 'Bookmark' being a PostType! Read more about it at [the documentation](http://posttypes.readthedocs.org/en/develop/).

### Tutorials

* [Authorization Tutorial](Authorization.md) - This tutorial explains how to handle authorization quickely.

### Some suggestions

* Under 'Components' you can find many useful components like [Menu](../Components/Menu.md), or [IsAuthorized](../Components/IsAuthorized.md).
* Under 'Behaviors' you can find many useful behaviors like [WhoDidIt](../Behaviors/WhoDidIt.md), or [IsAuthorized](../Behaviors/IsAuthorized.md).
