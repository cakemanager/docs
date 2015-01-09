Authorization
=============

AuthComponent
-------------

When you load the `ManagerComponent` in your `AppController`, it will automatically load the `AuthComponent` with default settings.
You can change the settings via:

    $this->Manager->config('components.Auth', *settings*);

If you want to disable the AuthComponent for loading it by yourself use:

    $this->Manager->config('components.Auth', false);


RolesAuthorize
--------------

Instead of the `ControllersAuthorize`, the CakeManager uses the `RolesAuthorize`.
This Authorize checks on default prefixes (like admin), and checks if users are allowed (by role-definition) to that prefix.

If there is no prefix set, the `isAuthorize($user)` method will be requested from your controller.

> Note: The `isAuthorized`-method must exist, else an exception will raise.

Roles
-----

There are 4 default role-definitions:
- Administrators
- Moderators
- Users
- Unregistered

CakeManager has the following configuration:

    'CM.Roles' => [
        'Administrators' => [1],
        'Moderators' => [2],
        'Users' => [3],
        'Unregistered' => [4],
    ];
    
Remember CM automatically creates roles in your database? Here they are asigned to a role-definition of the CakeManager.
The CakeManager uses this role-definition to allow multiple roles (db) to a single role (app). Look at this example:

### Adding Roles to the Role-Definition

    If you want to allow Moderators to the admin-section;

    Configure::write('CM.Roles.Administrators', [1, 2]);
    
Now, the Moderators (id = 2) are added to the Administrator-definition. 

### Checking Role-Definitions

You can check if a user is allowed to a role-definition by the preset methods in the Manager-Component:

    $this->Manager->isAdmin($user);

This method will check if a user is allowed to the admin-section.

    $this->Manager->isModerator($user);

This method will check if a user is a moderator.

    $this->Manager->isUser($user);

This method will check if a user is a normal user.

    $this->Manager->isUnregistered($user);

This method will check if a user is a non-logged-in user.

> Note: Unregistered User means a non-logged-in user. This role can be usefull with ACL.


If you use the 'Roles-Authorize' from CM, it will automatically allow the Moderators to the admin-section.
