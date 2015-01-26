IsAuthorized-Behavior
==================

The IsAuthorized-Behavior is needed if you use the [IsAuthorized-Component](../Components/IsAuthorized.md). The IsAuthorized-Component allows you to to automatically check the authorization for editing and deleting posts.

Loading the Behavior
--------------------

You can load the behavior by the follwing code:

    public function initialize(array $config) {
        // code
        $this->addBehavior('CakeManager.WhoDidIt');
    }

### Options

The behavior will default validate on the `user_id` field. You can change the field with:

    public function initialize(array $config) {
        // code
        $this->addBehavior('CakeManager.WhoDidIt', [
          'field' => 'created_by' // changed the field
        ]);
    }
    
    
