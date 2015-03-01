Installation
============

This section gives a brief description how to install the CakeManager and it's requirements

Requirements
------------

You need to install a fresh copy of CakePHP 3.x. Read the [Quick Start](http://book.cakephp.org/3.0/en/quickstart.html) for more info.

You also need the [Migrations](https://github.com/cakephp/migrations) plugin from CakePHP itself. We asume it's autoloaded by CakePHP itself. The Crud-plugin is required by the CakeManager.

Getting the CakeManager
-----------------------

Using the inline require for composer:

    composer require cakemanager/cakephp-cakemanager:dev-master

Or add this to your composer.json configuration:

    "require": {
        "cakemanager/cakephp-cakemanager": "dev-master"
    }

After that we need to load our plugin in our `config/bootstrap.php`.

    Plugin::load('Utils', ['bootstrap' => true, 'routes' => true]);
    Plugin::load('CakeManager', ['bootstrap' => true, 'routes' => true]);

Creating the tables
--------------------

Schema's we know from CakePHP 2.x are not supported anymore. But we got the migrations-plugin from [CakePHP](https://github.com/cakephp/migrations).

Run the following command in your shell:

    $ bin/cake migrations migrate -p CakeManager
    
This command tells the Migrations-plugin to migrate (install) the CakeManager. This will load our tables.

Loading the roles and user
-----------------
We created a shell to load the default roles and adding an administrator. The CakeManager has the following subcommands:

**initialize**  
Execute The Initialize-method. This will add some important data to your database (like roles).

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
        $this->loadComponent('Utils.Authorizer'); // must have for your authorization
           
        // code
        
    }

### Configuring the Manager

There are multiple configurations for the manager-component.
See the [Manager Component](components/manager.md) for detailed documentation about the Manager-component.

Further reading
-------

You just started with the CakeManager.

Here are some suggestions related to this section:

- CakePHP's [Quick Start](http://book.cakephp.org/3.0/en/quickstart.html) for 3.x.
- Read the [Manager Component](components/manager.md) for detailed documentation about the Manager-component.
- Read the [Request Flow](request-flow.md) for detailed documentation about callbacks and events via the CakeManager.
- Read the [Configurations](configurations.md) for detailed documentation about the available configurations of the plugin.
- Read the [Utils Docs](http://cakemanager-utils.readthedocs.org/en/latest) for documentation about all components and behaviors.
