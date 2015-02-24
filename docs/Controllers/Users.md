UsersController
===============

The `UsersController` handles most of the login-actions. 


Actions
-------

The following actions are available:

- login
- activate
- request
- new_password
- logout

### Login

This method logs the user in. After the user is logged in he will be redirected to the given url of his role. 
In the CakeManager you are able to set the redirect-url per role.
If an login fails, it will redirect to its referer action. 
This is because you maybe want to use your own login-actions, but use the logic of the CakeManager.

### Activate

This method activates a new account. When an user is registerd it will receive an email with an url. 
That url will redirect to this activation-action. This action requires two values: `email` and `activation_id`. Example:

```
http://domain.org/user/activate/admin@cakemanager.org/8asdfnqSDzxmAKcn237KJHf
```

### Request

The request-action is used to set a new `activation_key` for the user. The user has to input his e-mailaddress.
When the key is set, he is still able to login, however, he will receive an email to set a new password.

### New Password

The new_password-action is used to let the user set a new password. 
This action requires two values: `email` and `activation_id`. Example: 

```
http://domain.org/user/new_password/admin@cakemanager.org/8asdfnqSDzxmAKcn237KJHf
```

After the new password is set, it will redirect to the login-action. When the action fails, it will return to it's referer action.

### Logout

This method logs the user out. It's a simple piece of code ;). The redirection is chosen by the `AuthComponent`.
Use the following to change it's redirect:

```php
  // in your AppController::initialize()
  $this->Auth->config('logoutRedirect', 'redirect_string_or_array');
```

Customizing
-----------

If you want to use your own views and actions, you are free to go. These actions are also available for the logic. 
That means that you are able to use the login-action (from CM) only for it's POST, and use your own action for the view.
Remember that you have to set the action-attribute of your login-form to the login-action of the CakeManager.
The same is applied to the other actions.


