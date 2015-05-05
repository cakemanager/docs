EmailListener-Component
====================

The `EmailListenerComponent` contains some methods and events to send e-mails.

[doc_toc]


Loading
-------

You can load the component in your AppController:

            public function initialize() {
                // code
                $this->loadComponent('CakeManager.EmailListener');
            }


All types of E-mails
--------------------

The following e-mails will be send:

### Activation

When a new user is created (by administrators or the user itself) and activation is enabled, an activationmail will
be sent. This e-mail will contain the most important information including an activation-url. When clicking on it,
the user will be activated and able to login.

### Activation Confirmation

When the user has activated its account successfully an activation confirmation will be sent.

### Forgot Password

When someone forgot its password, and sent the form this e-mail will be sent. The user will receive an e-mail with a 
link to set a new password.

### Password Confirmation

After setting up a new password the user will receive a confirmation of the new password. Also when an administrator 
changes the password for a specific user, it will receive a notification about that.


Configurations
--------------

All e-mail functions above contain the same configurations. All configurations are accessible via 
`Configure::read('CM.Mail')`. Every mail-type has its own configurations:

- `CM.Mail.activation`
- `CM.Mail.activationConfirmation`
- `CM.Mail.forgotPassword`
- `CM.Mail.passwordConfirmation`

### Configurations per type

Every type has the same configurations:

#### Subject
The `subject` configuration is used to set the subject of the e-mail. Example:

        Configure::write('CM.Mail.activation.subject', 'Hey there!');

This code will set the subject 'Hey there!' as activation-mail.

#### Layout
The `layout` configuration is used to set the layout-file wich is default `CakeManager.base`. If you want to use your 
own layout-file you could use the following example:

        Configure::write('CM.Mail.activation.layout', 'customLayout');

#### Template
The `template` configuration is used for the template file. This option can be useful when you want to use your own
text in your e-mails. Example to use your own templates:

        Configure::write('CM.Mail.activation.template', 'activationCustom');

### Disabeling e-mails

You can easily disable e-mails by setting the specific configuration to `false`. Example:

        Configure::write('CM.Mail.activationConfirmation', false);

No confirmation-emails will be sent anymore!

### Overall configurations

There are some overall configurations available:

- `transport` - The transport that should be used for the e-mails. 
http://book.cakephp.org/3.0/en/core-libraries/email.html#using-transports
- `sender` - An array with the `name` and `email` of the sender. Example:
        'sender' => [
            'email' => 'no-reply@mymail.com',
            'name' => 'CakeManager'
        ],
- `from` - The `from` key of the `Email`-class. 
http://book.cakephp.org/3.0/en/core-libraries/email.html#configuration-profiles


Sending e-mails manually
------------------------

Maybe in some cases you want to send an activation-mail or something manually. This is very easy for the `EmailListener`.
Use the following code in your controller:

        $this->EmailListener->activation($user);

`$user` should be an array with the userdata. The following methods are available:

- `EmailListenerComponent::activation($user)`
- `EmailListenerComponent::activationConfirmation($user)`
- `EmailListenerComponent::forgotPassword($user)`
- `EmailListenerComponent::passwordConfirmation($user)`