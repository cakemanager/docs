Authorization
=============

In this section we will talk about how authorization is managed by the CakeManager. 
A short summary: 

* The `ManagerComponent` automatically loads the [`AuthComponent`](#authcomponent).
* Because CakeManager uses `ControllerAuthorize` we built a [RoleBased `AuthorizerComponent`](#rolebased-authorization).
* To easily manage your roles (for plugins) we use [Role-Definitions](#role-definitions)


AuthComponent
-------------

When you load the `ManagerComponent` in your `AppController`, it will automatically load the `AuthComponent` with default settings.
You can change the settings via:

    $this->Manager->config('components.Auth', *settings*);

If you want to disable the AuthComponent for loading it by yourself use:

    $this->Manager->config('components.Auth', false);


RoleBased Authorization
-----------------------

We use as default the `ControllerAuthorize` from Cake itself. That means authorization will be done by the controllers method `isAuthorized`. We have built a role-based helper-component for this way. [Check it out!](Components/Authorizer.md)

> Note: The `isAuthorized`-method must exist, else an exception will raise.

Role-Definitions
----------------

What the hell are Role-Definitions? Well look... We are planning some great plugins, and our goal is to make as easy as possible for you. So, when you have a big plugin and you need to do some stuff with multiple roles, we need to easily get default roles! Thats why you register your 'database'-roles. You can create as many as you want. But, there are 4 default Role-Definitions.

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
    
Remember CM automatically creates roles in your database? Here they are asigned to a Role-Definition of the CakeManager.
The CakeManager uses this Role-Definition to allow multiple roles (db) to a single role (app). Look at this examples:

### Adding Roles to the Role-Definition

    If you want to allow Moderators to the admin-section;
    Configure::write('CM.Roles.Administrators', [1, 2]);
    
Now, the Moderators (id = 2) are added to the Administrator-definition. 

### Checking Role-Definitions

You can check if a user is allowed to a Role-Definition by the preset methods in the Manager-Component:

    $this->Manager->isAdmin($user);

This method will check if a user is allowed to the admin-section.

    $this->Manager->isModerator($user);

This method will check if a user is a moderator.

    $this->Manager->isUser($user);

This method will check if a user is a normal user.

    $this->Manager->isUnregistered($user);

This method will check if a user is a non-logged-in user.

> Note: Unregistered User means a non-logged-in user. This role can be usefull with ACL.

### Using Role-Definitions

Role-Definitons can be usefull when you use a big plugin who uses multiple roles. They will be able to use your definitions for your application. You can get definitions by the following.

    // getting the administrator-roles
    Configure::write('CM.Roles.Administrators');
    
`Administrators` can be replaced by `Moderators`, `Users` and `Unregistered`.
