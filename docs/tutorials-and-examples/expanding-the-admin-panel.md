Expanding the Admin-panel
=========================

You are probably all set, your CakeManager is running, and now you want to expand your area with your own code.
In this example you'll learn how to do that, and how flexible the CakeManager is.

[doc_toc]


Prefixes
--------

Prefixes are very important. The CakeManager listens to the prefix `admin`. That means that your own code, without
prefix won't be hurt by the CakeManager.

Controllers
-----------

Of course you need your own controllers for the admin-area. This can be done by adding your controllers with the 
`admin` prefix. Look at this example:

        <?php
        // src/Controller/Admin/BookmarksController.php

        namespace App\Controller\Admin;

        use App\Controller\AppController;

        class BookmarksController extends AppController
        {
            public function isAuthorized($user) {
                $this->Authorizer->action(['*'], function ($auth) {
                    $auth->allowRole(1); // only allow administrators
                });
                
                return $this->Authorizer->authorize();
            }
        }

You see that the namespace ends with `\Admin`. This is all you need, the CakeManager will do its stuff automatically.

When you need your own controllers for your front-end (so not your admin-panel) just do as normally!


Menu-items
----------

Your controller has been made, now we need a menu-item to move to it. This code can be placed in your `AppController`.

        public function initMenuItems() {
            $this->Menu->add('Bookmarks', [
                'url' => [
                    'plugin' => false,
                    'prefix' => 'admin',
                    'controller' => 'bookmarks',
                    'action' => 'index'
                ]
            ]);
        }

The `initMenuItems`-method is automatically called by the `MenuComponent`. The `add`-method will add a new item to the menu.


Done
----

Well done! You've added your own controller, and are able to expand your admin-panel. Good luck with coding ;)


Further reading
---------------

* [Authorization](/docs/1.0/tutorials-and-examples/authorization) is really important for your app!
