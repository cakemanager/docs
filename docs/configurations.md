Configurations
==============

This page tells something about the available configurations you can use (config/bootstrap.php).

Bootstrap
---------

Configurations are loaded in the `CakeManager/config/bootstrap.php`. You can override them by setting your own values after loading the `bootstrap.php`.

Configurations
--------------

### Register

With the `CM.Register` configure you enable or disable the register-form at `/register`. This configure is defaultly 
set to `false` to prevent unwanted users on your system. Example to enable registrations:

        Configure::write('CM.Register', true);

### ActivationOnRegister

When you have register enabled, you can use this configure to let your users active their account via an e-mail. This
configure is default set to `true` to prevent unwanted users. Note that you need a mail-service on your server.
Example to disable this configuration:

        Configure::write('CM.ActivationOnRegister', false);

### Roles

The `CM.Roles`-configuration is an role-definition-array. [later more]

        Configure::read('CM.Roles');

        // Would return:
        [
            'Administrators' => [
                (int) 0 => (int) 1
            ],
            'Moderators' => [
                (int) 0 => (int) 2
            ],
            'Users' => [
                (int) 0 => (int) 3
            ],
            'Unregistered' => [
                (int) 0 => (int) 4
            ]
        ]

### UserModel

You can change the `CM.UserModel` if you want to use your own UserModel.

        Configure::read('CM.UserModel');

        // Would return

        'CakeManager.Users'

### UserViews

The CakeManager has default view-files for the UsersController. 
If you want to change them, you can change it this way:

    Configure::write('CM.UserViews.login`, '/myPath/myFile');
    
Note that `CM.UserViews` is an array with a list of all actions.

Current actions:
- register
- login
- forgot_password
- reset_password

        Configure::read('CM.UserViews');

        // Would return

        [
            'login' => 'CakeManager./Users/login',
            'forgot_password' => 'CakeManager./Users/forgot_password',
            'reset_password' => 'CakeManager./Users/reset_password'
        ]

### Admin UserViews

The CakeManager has default view-files for the UsersController (admin). The following actions are rendered:

- index
- view
- add
- edit
- new_password

### Admin RoleViews

The CakeManager has default view-files for the RolesController (admin). The following actions are rendered:

- index
- view
- add
- edit

### Mail

The CakeManager is able to send mails automatically when an user has been registered, or requests a new password.

        Configure::read('CM.Mail');

        // Would return

        [
            'From' => [
                'noreply@cakemanager.org' => 'CakeManager'
            ],
            'afterLogin' => true
        ]

The CakeManager automatically sends a mail on the callback `afterLogin`. If you want to disable that event, use:

        Configure::write('CM.Mail.afterLogin', false);

The `From`-key is to define the `from()` of the `Mail`-class. The mail is default sent from `noreply@cakemanager.org` but can be changed:

        Configure::write('CM.Mail.From', ['info@cakemanager.org' => 'CakeManager Suport']);

> Note: This features are in early development and not completely supported
