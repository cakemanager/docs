UsersModel
==========

The `UsersTable` and `User`-Entity are the default models used by CakePHP.
In this section we will explain what the model does and how to implement your own model.

[doc_toc]

UsersTable
----------

The `UsersTable` contains several methods related to creating and validating users.
This methods are available:
- `generateActivationKey` - Generates an activation key for an user.
- `validateActivationKey` - Checks if an user is related to the key.
- `activateUser` - Validates the activation key and activates the user.

The class also contains some basic validation. 
See the API for detailed info about the validation.

User Entity
-----------

The `User` Entity keeps the fields that can be mass assigned and hashes the password if 
set. Note that the `password` field is hidden when returning a json-array or something.

Customizing the UsersModel
--------------------------

The CakeManager delivers the default UsersModel but of course we want you to give you 
the possibility to use your own model.

> Note: Use `$ bin/cake bake model Users` to generate the UsersModel quickely.

It's very simple. Just create your own UsersTable like:

    namespace App\Model\Table;

    use CakeManager\Model\Table\UsersTable as BaseUsersTable;
    use Cake\Validation\Validator;

    /**
     * Users Model
     */
    class UsersTable extends BaseUsersTable
    {
        public function initialize(array $config)
        {
            parent::initialize($config);
        }
    }

And this is an example for your Entity:

    namespace App\Model\Entity;
    
    use CakeManager\Model\Entity\User as BaseUser;
    
    /**
     * User Entity.
     */
    class User extends BaseUser
    {
        // your custom accessibles
    }

Note that we extended the class to `BaseUsersTable` and not `Table`. 
This helps you to use the default `UsersTable` from CakeManager, but will always
override your stuff if you put it in your own `UsersTable`.
That's the same for the Entity.

We are almost done. Use this in your `config/bootstrap.php`:

    Configure::write('CM.UserModel', 'Users');

The default value is `CakeManager.Users`. By using this value your customized 
`UsersTable` will be used.
