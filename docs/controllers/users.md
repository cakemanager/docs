UsersController
===============

The `UsersController` handles most of the login-actions. They will be explained in 
this section. We also give you some tips and tricks to customize the `UsersController`
to your own controller.

[doc_toc]

Actions
-------

The following actions are available:

- register
- login
- activate
- forgotPassword
- resetPassword
- logout

### Register

The register-action is used to register new users. New users will default carry the role `3`.
That means that it's a normal user.

If you don't want visitors to register you can disable the registration-option in your 
`config/bootstrap.php`:

        Configure::write('CM.Register', false);

Default new users will have to activate their account via an e-mail (sent by the CM). You can 
disable this option via the `config/bootstrap.php`:

        Configure::write('CM.ActivationOnRegister', false);

In this case no mail will be sent to the new user, and the users won't have to active its account.

Available events:

- [Controller.Users.afterRegister](/docs/1.0/callbacks/#controllerusersafterregister)
- [Controller.Users.afterInvalidRegister](/docs/1.0/callbacks/#controllerusersafterinvalidregister)

### Login

This method logs the user in. After the user is logged in he will be redirected to 
the given url of his role. In the CakeManager you are able to set the redirect-url 
per role. If an login fails, it will redirect to its referer action. This is because 
you maybe want to use your own login-actions, but use the logic of the CakeManager.

Available events:

- [Controller.Users.afterLogin](/docs/1.0/callbacks/#controllerusersafterlogin)
- [Controller.Users.afterInvalidLogin](/docs/1.0/callbacks/#controllerusersafterinvalidlogin)

### Activate

This method activates a new account. When an user is registerd it will receive an 
email with an url. That url will redirect to this activation-action. This action 
requires two values: `email` and `activation_id`. Example:

```
http://domain.org/user/activate/admin@cakemanager.org/8asdfnqSDzxmAKcn237KJHf
```

Available events:

- [Controller.Users.afterActivate](/docs/1.0/callbacks/#controllerusersafteractivate)

### Forgot Password

The request-action is used to set a new `activation_key` for the user. The user has 
to input his e-mailaddress. When the key is set, he is still able to login, however,
he will receive an email to set a new password.

Available events:

- [Controller.Users.afterForgotPassword](/docs/1.0/callbacks/#controllerusersafterforgotpassword)

### Reset Password

The new_password-action is used to let the user set a new password. This action 
requires two values: `email` and `activation_id`. Example: 

```
http://domain.org/user/resetPassword/admin@cakemanager.org/8asdfnqSDzxmAKcn237KJHf
```

After the new password is set, it will redirect to the login-action. When the action 
fails, it will return to it's referer action.

Available events:

- [Controller.Users.afterResetPassword](/docs/1.0/callbacks/#controllerusersafterresetpassword)

### Logout

This method logs the user out. It's a simple piece of code ;). The redirection is 
chosen by the `AuthComponent`. Use the following to change it's redirect:

```php
  // in your AppController::initialize()
  $this->Auth->config('logoutRedirect', 'redirect_string_or_array');
```

Changing the views
------------------

The CakeManager is using it's own views for these actions. Of course you are able to 
change them. In your `config/bootstrap.php` file you can change some configures for 
rendering other view-files

Available view-files:

- register
- login
- forgotPassword
- resetPassword

Let's show some examples:

```
  // changing all the views
  Configure::write('CM.UserViews', [
      'login'           => '/CustomUsers/login',
      'forgotPassword' => '/CustomUsers/forgot_password',
      'resetPassword'  => '/CustomUsers/reset_password',
  ]);

  // changing the login only
  Configure::write('CM.UserViews.login', '/CustomUsers/login');

```

Now you have to create your view-files like `Templates/CustomUsers/login.ctp`. You 
can find the default view-files [here](https://github.com/cakemanager/cakephp-cakemanager/tree/master/src/Template/Users). 
Copy them to get a good base for your layout.

Custom UsersController
----------------------

Maybe you want to use your own `UsersController`, so you are free to go! Here are 
some tips.

### Controller

First of all you need your own controller. To inherit the base-actions of the CakeManager, 
here's an example:

```php
    namespace App\Controller;
  
    use CakeManager\Controller\UsersController as CMUsersController;
    
    class UsersController extends CMUsersController
    {
    
        public function beforeFilter(\Cake\Event\Event $event)
        {
            // set your own layout and theme
            $this->layout = "guest";
            $this->theme = "";
    
            // don't forget to load the parent's beforeFilter
            parent::beforeFilter($event);
    
        }
    
        public function login()
        {
            // let's say you want to change some stuff here
    
            parent::login(); // loading the parents' login (CakeManager)
            
            // of course you are able to do stuff here too
        }
    
        public function custom()
        {
            // this action is completely yours!
        }    
    
    }
```

### Routing

Now your controller is set, we need to let our routers know we have chosen another 
controller:

    // in your config/routes.php
    Router::connect('/users/:action/*', [
        'plugin' => false,
        'prefix' => false,
        'controller' => 'Users',
    ]);
    
This code tells the router to connect to your own controller (UsersController).



