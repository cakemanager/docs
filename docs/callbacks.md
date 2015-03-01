Events and Callbacks 
=========

The CakeManager registers multiple callbacks. This is helpfull to make your app flexible.
Plugins are able to do stuff automatically, and you are able to keep your code clean.

All callbacks will be documented in this section.

To get a clear view about the request-flow, read [this section: Request Flow](request-flow.md).

Components
==========

## Manager

## Component.Manager.beforeFilter

This event is requested before the original `beforeFilter`-event of the controller, but will be fired after the component's `beforeFilter`-event. This can be usefull to load components in your plugin before the user will need to use them. (Else you'll be too late loading it because the user needs it ;))

## Component.Manager.beforeFilter.prefix

`prefix` has to be replaced with the current prefix of the request.
This event is requested after the default `Component.Manager.beforeFilter`-event.

## Component.Manager.startup

This event will be fired after the component's  `startup`-event, but before the actionlogic.

## Component.Manager.startup.prefix

`prefix` has to be replaced with the current prefix of the request.
The same as above, but specified for prefixes. Can be usefull if you want to do something for admin only. This event will be fired after the normal `startup`-event.

## Component.Manager.beforeRender

This event is called after the component's `beforeRender`-event, but before the controller's one.

## Component.Manager.beforeRender.prefix

`prefix` has to be replaced with the current prefix of the request.
This is the same as above, but specified for prefixes.
This event is called after the `beforeRender` callback of the `ManagerComponent`.

## Component.Manager.shutdown

Called after the component's `shutdown`-event, and before the action-render-method from CakePHP itself.

## Component.Manager.shutdown.prefix

`prefix` has to be replaced with the current prefix of the request. This is the same as above but specified for prefixes.


Controllers
===========

There are no events registered for the controllers, but we will add some events soon!

To Do:

- AfterLogin
- AfterRequest
- AfterActivate
- AfterNewPassword
- AfterRegister (first we have to make a register-functionality)
