Installation
============

This section gives a brief description how to install the CakeManager and it's requirements

Requirements
------------

You need to install a fresh copy of CakePHP 3.x. Read the [Quick Start](http://book.cakephp.org/3.0/en/quickstart.html) for more info.

You also need the [Migrations](https://github.com/cakephp/migrations) plugin from CakePHP itself. We asume it's autoloaded by CakePHP itself.

Installing CakeManager
----------------------

We asume you already got a new project of CakePHP. You can call the plugin via composer:

    "cakemanager/cakephp-cakemanager": "dev-master"

After that we need to load our plugin in our config/bootstrap.php. We also need the Migrations-plugin from CakePHP to load our tables. Also the [Crud-Plugin](https://github.com/FriendsOfCake/crud/tree/cake3) is required by the CakeManager.

    Plugin::load('CakeManager', ['bootstrap' => true, 'routes' => true]);
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
----------

After loading the plugin we have to load the base-component `CakeManager.Manager`.

    public function initialize() {
        
        // code
        
        $this->loadComponent('CakeManager.Manager');
        $this->loadComponent('CakeManager.Authorizer'); // must have for your authorization
        $this->loadComponent('CakeManager.IsAuthorized'); // should have for your authorization
           
        // code
        
    }

### Configuring the Manager

There are multiple configurations for the manager-component.
See the [Manager Component](Components/Manager.md) for detailed documentation about the Manager-component.

Further reading
-------

You just started with the CakeManager.

Here are some suggestions related to this tutorial:

- CakePHP's [Quick Start](http://book.cakephp.org/3.0/en/quickstart.html) for 3.x.
- Read the [Manager Component](Components/Manager.md) for detailed documentation about the Manager-component.
- Read the [Request Flow](Request-Flow.md) for detailed documentation about callbacks and events via the CakeManager.
- Read the [Configurations](Configurations.md) for detailed documentation about the available configurations of the plugin.
