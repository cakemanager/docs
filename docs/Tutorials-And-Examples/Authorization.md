Authorization
=============

We want to register our authorization easily. We gonna help you!

Loading the Component
---------------------

We've built the `AuthorizerComponent`. This component helps you defining authorization in your `isAuthorized()`-method. For more, read the [documentation [Utils plugin]](http://cakemanager-utils.readthedocs.org/en/develop/components/authorizer/).

Load the component in your `AppController` by using:

    public function initialize() {
        
        // code
        
        $this->loadComponent('CakeManager.Manager');
        $this->loadComponent('CakeManager.Authorizer');
        
        // code
    }

Defining per controller
-----------------------

Now we gonna define our authorization per controller. Lets take an example for 'any' `PostsController`.

    public function isAuthorized($user) {
        
        // allows adminstrators (1) to all actions (*)
        $this->Authorizer->action(['*'], function($auth) {
            $auth->allowRole([1]);
        });
        
        // This part is under construction
        //  // Moderators (2) can only view, edit and delete their own posts
        //  $this->Authorizer->action(['view', 'edit', 'delete'], function($auth) {
        //      $auth->setRole([2], $this->IsAuthorized->authorize());
        //  });
        
        // Moderators (2) are ALSO able to add posts
        $this->Authorizer->action(['add'], function($auth) {
            $auth->allowRole([2]);
        });
        
        return $this->Authorizer->authorize();
    }

Thats it! Hopefully the comments explain it's code. For more info you can read the [documentation [Utils plugin]](http://cakemanager-utils.readthedocs.org/en/develop/components/authorizer/) about the `AuthorizerComponent`.

Further Reading
---------------

If you want to know more about the authorization of the CakeManager, read the [Authorization Section](../Authorization.md).

Components used in this section:

* [Authorizer [Utils plugin]](http://cakemanager-utils.readthedocs.org/en/develop/components/authorizer/) - Tool to make Authorization easier.

Behaviors used in this section:

