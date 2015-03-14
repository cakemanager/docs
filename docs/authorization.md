Authorization
=============

In this section we will talk about how authorization is managed by the CakeManager. 

[doc_toc]

AuthComponent
-------------

When you load the `ManagerComponent` in your `AppController`, it will automatically 
load the `AuthComponent` with default settings. You can change the settings via:

    $this->Manager->config('Auth', *settings*);

If you want to disable the AuthComponent for loading it by yourself use:

    $this->Manager->config('Auth', false);


RoleBased Authorization
-----------------------

We use as default the `ControllerAuthorize` from CakePHP itself. That means 
authorization will be done by the controllers method `isAuthorized`. We have built a 
role-based helper-component for this way. [Check it out!](http://cakemanager.org/docs/utils/1.0/components/authorizer/)

> Note: The `isAuthorized`-method must exist, else an exception will raise.

Role-Definitions
----------------

What are role-definitions? Well look... The CakeManager has 4 default roles:

- Administrators
- Moderators
- Users
- Unregisterd (will be helpfull with acl)

It's helpfull to use these roles for your application, but what if we talk about 
flexibility? Maybe you need some extra roles, but external plugins won't be able to 
recognize them. Thats why we use role-definitions. They are equal to the default roles 
of the CakeManager, but you are able to assign your own roles to the role-definitions. 
Long talk, but look at this example.

### Example

This are the 4 registered role-definitions:

- Administrators
- Moderators
- Users
- Unregistered

The roles of the CakeManager are defined this way:

    'CM.Roles' => [
        'Administrators' => [1],
        'Moderators' => [2],
        'Users' => [3],
        'Unregistered' => [4],
    ];
    
But what if we want some new roles:

- Teacher (id: 5)
- Student (id: 6)

We can add these roles to the role-definition 'Users'.

    Configure::write('CM.Roles.Users', [5,6])
    
Now Teacher and Student are added to the role-definition of Users.

### Checking Role-Definitions

You can check if a user is allowed to a Role-Definition by the preset methods in the 
Manager-Component:

    $this->Manager->isRoledefinition("Administrators", $user);


### Using Role-Definitions

Role-Definitons can be usefull when you use a big plugin who uses multiple roles. 
They will be able to use your definitions for your application. You can get 
definitions by the following.

    // getting the administrator-roles
    Configure::read('CM.Roles.Administrators');
            
    // getting the moderator-roles
    Configure::read('CM.Roles.Moderators');
        
    // getting the users-roles
    Configure::read('CM.Roles.Users');
                
    // getting the unregistered-roles
    Configure::read('CM.Roles.Unregistered');
    
