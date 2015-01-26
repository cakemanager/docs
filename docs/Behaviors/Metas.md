Metas-Behavior
==================

The Metas-Behavior can be used to add custom meta-data to your entities without creating an extra column. 
This can be useful when you build things that are extendable (like plugins).

Loading
-------

You can load the behavior by the follwing code:

      public function initialize(array $config) {
          // code
          $this->addBehavior('CakeManager.Metas');
      }

Registering the Getters and Setters
--------------------

We made it as easy as possible for you to add meta-fields. Wouldn't it be great if you could treath your meta-fields just like the default fields of your table?
To do that you have to add `getters` and `setters` in your `Entity`.

        protected function _getCustomfield() {
            $model = TableRegistry::get('Bookmarks');
            return $model->registerGetter($this, 'customfield');
        }
    
        protected function _setCustomfield($value) {
            $model = TableRegistry::get('Bookmarks');
            $this->metas = $model->registerSetter($this, 'customfield', $value);
        }
        
Now you are able to get and set your `customfield`.

Some examples:

        // getting the customfield
        echo $entity->customfield;
        
        // form-field for the meta-field
        echo $this->Form->input('customfield');
        
        // setting the customfield
        $entity->customfield = "My Value";
        

        
