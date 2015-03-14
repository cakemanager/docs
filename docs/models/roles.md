RolesModel
==========

Just like the `UsersTable` the `RolesTable` is defined by the CakeManager and is editable
by you.

[doc_toc]

RolesTable
----------

The `RolesTable` has only one special method:
- `redirectFrom` - This method is used to redirect an user based on its role id.

The Table class handles the default validation. That means that 'name' is required.

Role Entity
-----------

The `Role` Entity keeps the fields that can be mass assigned.

Customizing the RolesModel
--------------------------

At the moment you are not able to customize the RolesModel to your own... We don't expect
you to do that, but in feature we want to give you the possibility to do that.