Manager-Component
====================

[doc_toc]


Loading
-------

You can load the component in your AppController:

            public function initialize() {
                // code
                $this->loadComponent('CakeManager.Manager');
            }

The ManagerComponent is the heartbeat of the plugin. This component adds several callbacks and events, and registers the default values for the AuthCompnent to add authorization to your application. In this section we will explain some configurations and we will give some tips and tricks to increase the flexibility of your application.

Configurations
--------------

There are multiple configurations for your application:

### Auth
The Auth-configuration contains the settings for the AuthComponent, loaded by the Cakemanager.
An example of the default configurations:

            'authorize'            => 'Controller',
            'userModel'            => 'CakeManager.Users',
            'authenticate'         => [
                'Form' => [
                    'fields' => [
                        'username' => 'email',
                        'password' => 'password'
                    ],
                    'scope'  => ['Users.active' => true],
                ]
            ],
            'logoutRedirect'       => [
                'prefix'     => false,
                'plugin'     => 'CakeManager',
                'controller' => 'Users',
                'action'     => 'login'
            ],
            'loginAction'          => [
                'prefix'     => false,
                'plugin'     => 'CakeManager',
                'controller' => 'Users',
                'action'     => 'login'
            ],
            'unauthorizedRedirect' => false,
            
This settings can be changed by the following example:

    // in your AppControllers initialize-method
    $this->loadComponent('CakeManager.Manager', [
        'Auth' => [
            'UserModel' => 'MyCustomUserModel'
        ]
    ]);
    
The Users model can be extended and used alongside another model such as UserDetails:

    // in your AppControllers initialize-method
    $this->loadComponent('CakeManager.Manager', [
        'Auth' => [
                'authenticate' => [
                    'Form' => [
                        'contain' => [
                            'UserDetails'
                        ]
                    ]
            ]
        ]
    ]);
    
If you don't want to let the `ManagerComponent` loading the `AuthComponent`, use the following code:

    // in your AppControllers initialize-method
    $this->loadComponent('CakeManager.Manager', [
        'Auth' => false
    ]);
    
The `AuthComponent` won't be loaded anymore, and you are free to add your own `AuthComponent`.

### adminTheme

The admin-area is using a custom theme by the CakeManager, but maybe you want to change it. Use this key to choose your own theme:

    // in your AppControllers initialize-method
    $this->Manager->config('adminTheme', 'myCustomTheme');

### adminLayout

The admin-area is using a custom layout-file by the CakeManager, but maybe you want to change it. Use this key to choose your own layout-file:

    // in your AppControllers initialize-method
    $this->Manager->config('adminLayout', 'myCustomLayoutFile');

### adminMenus

This part is still in development, we are looking for a clean way to initialize helpers for custom menu-items.
Currently there are multiple menu-areas available. Think about main, navbar, footer, and more. For each area you want another layout. The layout for menu's is defined by helpers. This config gives you the possibility to add a helper to a menu-area.

Example:

    // in your AppControllers initialize-method
    $this->Manager->config('adminMenus.main', 'MainMenu');
    
Available menu-areas: main and navbar


Events and Callbacks
--------------------

The `ManagerComponent` registers many callbacks and events witch are documented on the [Callbacks-page](/docs/1.0/callbacks).
