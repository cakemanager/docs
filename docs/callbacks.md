Callbacks and Events
====================

The CakeManager registers multiple callbacks. This is helpfull to make your app flexible.
Plugins are able to do stuff automatically, and you are able to keep your code clean.

All callbacks will be documented in this section.

To get a clear view about the request-flow, read [this section: Request Flow](docs/1.0/request-flow).


[doc_toc]

Components
----------

### Component.Manager.beforeFilter

This event is requested before the original `beforeFilter`-event of the controller, but will be fired after the component's `beforeFilter`-event. This can be usefull to load components in your plugin before the user will need to use them. (Else you'll be too late loading it because the user needs it ;))

### Component.Manager.beforeFilter.prefix

`prefix` has to be replaced with the current prefix of the request.
This event is requested after the default `Component.Manager.beforeFilter`-event.

### Component.Manager.startup

This event will be fired after the component's  `startup`-event, but before the actionlogic.

### Component.Manager.startup.prefix

`prefix` has to be replaced with the current prefix of the request.
The same as above, but specified for prefixes. Can be usefull if you want to do something for admin only. This event will be fired after the normal `startup`-event.

### Component.Manager.beforeRender

This event is called after the component's `beforeRender`-event, but before the controller's one.

### Component.Manager.beforeRender.prefix

`prefix` has to be replaced with the current prefix of the request.
This is the same as above, but specified for prefixes.
This event is called after the `beforeRender` callback of the `ManagerComponent`.

### Component.Manager.shutdown

Called after the component's `shutdown`-event, and before the action-render-method from CakePHP itself.

### Component.Manager.shutdown.prefix

`prefix` has to be replaced with the current prefix of the request. This is the same as above but specified for prefixes.


Controllers
----------

### Controller.Users.afterRegister

This event is called after a new user registered.

**Data**
- `user` - An array with the userdata who registered.

### Controller.Users.afterInvalidRegister

This event is called after a new user could not register.

**Data**
- `user` - An array with the userdata who tried to register.

### Controller.Users.afterActivate

This event is called after an user activated his account.

**Data**
- `email` - The e-mailaddress of the activated user.

### Controller.Users.afterLogin

This event is called after the user has been logged in succesfully.

**Data**
- `user` - An array from the user who logged in

### Controller.Users.afterInvalidLogin

This event is called after the user could not login.

**Data**
- `user` - An array from the user who tried to login.

### Controller.Users.afterForgotPassword

This event is called after the user requested a new password

**Data**
- `user` - An array from the user who requested the new password

### Controller.Users.afterResetPassword

This event is called after the user reset his password.

**Data**
- `user` - An array from the user who reset his password.
