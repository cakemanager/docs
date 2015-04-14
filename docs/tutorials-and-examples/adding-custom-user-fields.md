Expanding the Admin-panel
=========================

This example shows you how to add your own columns of the users-table to the CakeManager

[doc_toc]

Prepare
-------

For this example, first you need your own `UsersTable` and `User`-entity. Follow http://cakemanager.org/docs/1.0/models/users/#customizing-the-usersmodel 
to learn how to do that.

Adding the fields
-----------------

When you are done with the previous step, the following is easy. You need to configure the `CM.UserFields`-key.
The changes should be done in `config/bootstrap.php`:

    Configure::write('CM.UserFields', [
        'first_field',
        'second_field' => [
            'type' => 'textarea'
        ]
    ]);

You can add as many fields as you want. When adding an array as value you are able to pass options, just like you do
when creating a form with the `FormHelper`.

> Note: http://cakemanager.org/docs/1.0/configurations/#userfields

Done
----

Well done! You've added your own fields to the user-panel. Good luck with coding ;)

