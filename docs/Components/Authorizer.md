Authorizer-Component
====================

The Authorizer-Component allows us to create easy authorization. You have to be familiar with the ControllerAuthorization from CakePHP. For more info see [The CookBook](http://book.cakephp.org/3.0/en/controllers/components/authentication.html#authorization)

This Component is role-based. You are not able (yet) to add specific auth-rules per user. (Except if you use the `setRole`-method.

Load the component with the following code:

    public function initialize() {
        // code
        $this->loadComponent('CakeManager.Authorizer');
    }
    
Configurations
--------------

### RoleField
The value `roleField` is default set to `role_id` this is the column / field of the role_id of the user in the session (`$this->Auth->user()`).

Before (CookBook)
------
This is an example from the CookBook:

      public function isAuthorized($user)
      {
          // All registered users can add articles
          if ($this->request->action === 'add') {
              return true;
          }
      
          // The owner of an article can edit and delete it
          if (in_array($this->request->action, ['edit', 'delete'])) {
              $articleId = (int)$this->request->params['pass'][0];
              if ($this->Articles->isOwnedBy($articleId, $user['id'])) {
                  return true;
              }
          }
      
          return parent::isAuthorized($user);
      }

We are using the `ControllerAuthorize`, so we have the method `isAuthorized` in our controller to define the authorization.

Using the Component
-------------------
Using the `Authorizer` gives us many tools to define our authorization clear. Look at this example:

      public function isAuthorized($user)
      {
          // All roles (we asume you got 4 roles) can add articles
          $this->Authorizer->action(['add'], function($auth) {
              $auth->allowRole([1,2,3,4]);
          });
      
          // The owner of an article can edit and delete it; except the admin (1)
          $this->Authorizer->action(['edit', 'delete'], function($auth) {
              // This is the IsAuthorized-Component from the CakeManager
              $auth->setRole([2,3,4], $this->IsAuthorized->authorize()); 
          });
          
          return $this->Authorizer->authorize();
      }

We combined this piece of code with the `IsAuthorized`-Component for autmatically checking if a Entity belongs to the logged in user.

Let's walk trough the code...

### Action-method
With the `action()`-method we can set restrictions to specific actions.
You can add one action like:

          $this->Authorizer->action(['add'], function($auth) {
              // code
          });

Or:

          $this->Authorizer->action('add', function($auth) {
              // code
          });

You can add multiple actions like:

          $this->Authorizer->action(['add', 'view', 'delete'], function($auth) {
              // code
          });
 
The second attribute is a function where you can add your rules per role. In this function you get the current component as attribute. So, in the example above you have the component under `$auth`.

### AllowRole and DenyRole
The `allowRole`- and `denyRole`-method is used to allow a role to the chosen action. Some examples:

          // Allow role 1, 2, 3 and 4 to the 'add' action
          $this->Authorizer->action(['add'], function($auth) {
              $auth->allowRole([1,2,3,4]);
          });
          
          // Allow role 1 to the 'add' action; the other roles will be set to false
          $this->Authorizer->action(['add'], function($auth) {
              $auth->allowRole([1]);
          });         
          
          // Same as above
          $this->Authorizer->action(['add'], function($auth) {
              $auth->allowRole([1]);
              $auth->denyRole([2]);
              $auth->denyRole([3]);
              $auth->denyRole([4]);
          });   

### SetRole
With the `setRole`-method you are able to depent your role-rule on your own methods. Some example:

          // Using the IsAuthorized-Component from the CakeManager
          $this->Authorizer->action(['add'], function($auth) {
              $auth->setRole([1,2,3,4], $this->IsAuthorized->authorize());
          });
          
          // Using your own method
          protected function ownMethod() {
              return false;
          }
          
          $this->Authorizer->action(['add'], function($auth) {
              $auth->setRole([1,2,3,4], $this->ownMethod());
          });

While this component is called `RoleBased` we're able to add `UserBased` auth-rules this way!
          
### Authorize
This is the final method of the component. This method checks if the current user is allowed to watch the requested action. Use this method like:

        return $this->Authorizer->authorize();
        
Further reading
---------------

Read more about the [IsAuthorized-Component](IsAuthorized.md).

You can follow a quick tutorial [here](./Tutorials-And-Examples/Authorization.md);
