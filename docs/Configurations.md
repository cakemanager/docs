Configurations
==============

This page tells something about the available configurations (config/bootstrap.php).

Bootstrap
---------

Configurations are loaded in the `CakeManager/config/bootstrap.php`. You can override them by setting your own values after loading the `bootstrap.php`.

Configurations
--------------

### Roles

The `CM.Roles`-configuration is an role-definition-array. [later more]

### UserModel

You can change the `CM.UserModel` if you want to use your own UserModel. This config has the default value: `CakeManager.Users`.

### UserViews

The CakeManager has default view-files. If you want to change them, you can change it this way:

    Configure::write('CM.UserViews.login`, '/myPath/myFile');
    
Note that `CM.UserViews` is an array with a list of all actions.

Current actions:
- login

### Admin UserViews

Same as above, but then for the admin-views. The following actions are available:
- index
- view
- add
- edit
- new_password

Example:

    Configure::write('CM.AdminUserViews.edit`, '/Admin/Users/edit'); 
    // this will refer to a own edit file, and not the `CakeManager.`-file
    
    
