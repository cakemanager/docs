Authorization
=============

We want to register our authorization easily. We gonna help you!

Loading the Component
---------------------

We've built the `AuthorizerComponent`. This component helps you defining authorization in your `isAuthorized()`-method. For more, read the [documentation](../Components/Authorizer.md).

Load the component in your `AppController` by using:

    public function initialize() {
        
        // code
        
        $this->loadComponent('CakeManager.Manager');
        $this->loadComponent('CakeManager.Authorizer');
        $this->loadComponent('CakeManager.IsAuthorized'); // Not required, but optionally
        
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
        
        // Moderators (2) can only view, edit and delete their own posts
        $this->Authorizer->action(['view', 'edit', 'delete'], function($auth) {
            $auth->setRole([2], $this->IsAuthorized->authorize());
        });
        
        // Moderators (2) are ALSO able to add posts
        $this->Authorizer->action(['add'], function($auth) {
            $auth->allowRole([2]);
        });
        
        return $this->Authorizer->authorize();
    }

Thats it! Hopefully the comments explain it's code. For more info you can read the [documentation](../Components/Authorizer.md) about the `AuthorizerComponent`.

Did you notice the following code: `$this->IsAuthorized->authorize()`? We'll explain next.

Protecting edits and deletes
----------------------------

Sometimes you have types where creaters are the only people who are able to edit and delete. Think about blogs. A moderator should only be able to edit and delete his own posts, and no others! CakePHP used the following code for that:

    public function isAuthorized($user)
    {
        
        // The owner of an article can edit and delete it
        if (in_array($this->request->action, ['edit', 'delete'])) {
            $articleId = (int)$this->request->params['pass'][0];
            if ($this->Articles->isOwnedBy($articleId, $user['id'])) {
                return true;
            }
        }
        
        return parent::isAuthorized($user);
    }
    
> Note: [See for the original documentation this URL](http://book.cakephp.org/3.0/en/tutorials-and-examples/blog-auth-example/auth.html#authorization-who-s-allowed-to-access-what).

We've built the `IsAuthorizedComponent` to make this proces automatically.

Register the `IsAuthorizedBehavior` in the used model:

        $this->addBehavior('CakeManager.IsAuthorized', [
            'field' => 'user_id',
        ]);
        
The `field`-option contains the field of the item who contains the users id. 

> Note: If you use the [WhoDidIt-Behavior](../Behaviors/WhoDidIt.md), set the `field` to `created_by`.

Now we are able to protect owners for its posts. Look at this example for your `isAuthorized()`-method in your `Controller`:

    public function isAuthorized($user) {
        
        // code
        
        // Moderators (2) can only edit and delete their own posts
        $this->Authorizer->action(['edit', 'delete'], function($auth) {
            $auth->setRole([2], $this->IsAuthorized->authorize()); // this method authorizes with our behavior!
        });
        
        // code
        
    }
    
Congratulations! You are done! From now on, Moderators only can edit and delete their own posts!

Further Reading
---------------

If you want to know more about the authorization of the CakeManager, read the [Authorization Section](../Authorization.md).

Components used in this section:

* [Authorizer](../Components/Authorizer.md) - Tool to make Authorization easier.
* [IsAuthorized](../Components/IsAuthorized.md) - Tool to protect owners of specific items.

Behaviors used in this section:

* [IsAuthorized](../Behaviors/IsAuthorized.md) - Tool to protect owners of specific items.
