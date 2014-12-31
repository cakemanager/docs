Quick Start
===========

The best way to experience and learn CakeManager is to sit down and build something. To start off we’ll build a simple bookmarking application, just like you did as first tutorial at [CakePHP](http://book.cakephp.org/3.0/en/quickstart.html).

Beginner Tutorial
===================
In this tutorial we will add our CakeManager. So, that means we will have our login-system, and will be able to use extra plugins to make our work easier

Getting the CakeManager
-----------------------
We asume you already got a new project of CakePHP. You can call the plugin via composer:

    "bobmulder/cakephp-cakemanager": "dev-master"

After that we need to load our plugin in our `config/bootstrap.php`. We also need the Migrations-plugin from CakePHP to load our tables.

    Plugin::load('CakeManager', ['bootstrap' => true, 'routes' => true, 'autoload' => true]);
    Plugin::load('Migrations');



Creating the tables
--------------------
Schema's we know from CakePHP 2.x are not supported anymore. But we got the migrations-plugin from [CakePHP](https://github.com/cakephp/migrations).

Run the following command in your shell:

    $ bin/cake migrations migrate -p CakeManager
    
This command tells the Migrations-plugin to migrate (install) the CakeManager. This will load our tables.

Loading the roles and user
-----------------
We created a shell to load the default roles and adding an administrator. You can access the shell via:

    $ bin/cake CakeManager.Init [command] [variables]

### Adding the roles
First we will add the roles:

    $ bin/cake CakeManager.Init Roles
    
This command creates the default roles of the CakeManager:
- Administrators
- Moderators
- Users
- Unregistered

### Adding an user
Now we need a administrator to login. Use the folling to register yourself:

    $ bin/cake CakeManager.Init Admin my_email@domain.com mypassword
    
- The first parameter is your e-mailaddress to login with.
- The second parameter is your (unhashed) password.

> Note: Submit a valid e-mailaddress, otherwise you won't be able to login (the validation requires an e-mailaddress)

> Note: If you get an error, the address already exists

Adding the component
--------------------

After loading the plugin we have to load the base-component: CakeManager.Manager.

        public function initialize() {
        
            // code
        
            $this->loadComponent('CakeManager.Manager');
        
            // code
        
        }

### Configuring the Manager

There are multiple configurations for the manager-component. 
See the [Manager Component](../Components/Manager.md) for detailed documentation about the Manager-component.

### Adding isAuthorized-method

If you reload your web-page you will probably get an error. Because we chose that the controller has to authorize, our `AppController` needs an isAuthorized-method.

    public function isAuthorized($user) {

        if ($this->IsAuthorized->behaviorIsset()) {
            return $this->IsAuthorized->authorize();
        }

        return true;
    }

Adding menu-items
-----------------

The admin-section uses the area 'main' for the default menu. Let's add an menu-item.
At first we create a new method in our `AppController` to store menu-items.

    public function adminMenuItems() {

        $this->Menu->add('My new Item', [
            'url' => [
                'plugin'     => false',
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

Having fun
---------
The CakeManager is set, we are now able to login, and manage our back-end. Go to yourdomain.com/login to login and start happy coding! 
Good luck!

Bob Mulder

The CakeManager-Team
