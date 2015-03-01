Request Flow
============

In this section we will give explanation about a default and - by the CakeManager extended - request-flow.

CakePHP
-------

This should be a normal request-flow by CakePHP:

Controller              | Component             | Events
:------------           | :-------------        | :------------
initialize              | ----                  | ----
----                    | beforeFilter          | ---- 
beforeFilter            | ----                  | ----
----                    | startup               | ---- 
= action logic =        | ----                  | ----
----                    | beforeRender          | ---- 
beforeRender            | ----                  | ----
----                    | shutdown              | ---- 
= action render =       | ----                  | ----            

> Note: The column 'Component' means all components

You can see that the common-used callbacks for the component like `beforeFilter` and `beforeRender` are surrounded by component-callbacks like `beforeFilter`, `startup`, `beforeRender` and `shutdown`. That means that if you want to do someting before the controllers `beforeFilter`, you need to do it in the components `beforeFilter`. But coming after the controllers `beforeFilter`, we use the components `startup`.

New Request-Flow by CakeManager
-------------------------------

This gave us a very clean way for our events:

| Controller              | Component             | Events                                  |
| :------------           | :-------------        | :------------                           |
| initialize              | ----                  | ----                                    |
| ----                    | beforeFilter          | ----                                    |
| ----                    | ----                  | Component.Manager.beforeFilter          |
| ----                    | ----                  | Component.Manager.beforeFilter.prefix   |
| beforeFilter            | ----                  | ----                                    |
| ----                    | startup               | ----                                    |
| ----                    | ----                  | Component.Manager.startup               |
| ----                    | ----                  | Component.Manager.startup.prefix        |
| = action logic =        | ----                  | ----                                    |
| ----                    | beforeRender          | ----                                    |
| ----                    | ----                  | Component.Manager.beforeRender          |
| ----                    | ----                  | Component.Manager.beforeRender.prefix   |
| beforeRender            | ----                  | ----                                    |
| ----                    | shutdown              | ----                                    |
| ----                    | ----                  | Component.Manager.shutdown              |
| ----                    | ----                  | Component.Manager.shutdown.prefix       |
| = action render =       | ----                  | ----                                    |

> Note: The column 'Component' means the ManagerComponent by CM; Events named after the component-callback are registered at the end of the component-event. Note that events may be called before your own components.

Why do we want to know this? This information can be useful if you want to fire your logic in an event before or after a specific callback of the controller.

You can automate your plugins by firing on events.
