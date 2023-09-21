# Backend
1. Installation de laravel
``composer create-projectl laravel/laravel <nom-du-projet>``
2. configuration de cors afin de supporter les informations d'authentification(cookies, jetons, etc)
```php
<?php

return [
///...
    'supports_credentials' => true,
///...
];
```
3. route/api.php
4. controller pour l'authentification
5. middleware d'auth. pour gestion de cookies et CSRF
   - ajout de EnsureFrontendRequestsAreStateful::class dans app/Http/Kernel.php
   ```php app/Http/Kernel.php
   protected $middlewareGroups = [
      //.........
        'api' => [
            \Laravel\Sanctum\Http\Middleware\EnsureFrontendRequestsAreStateful::class,
        //.........

        ],
    ];
   ```
# Frontend

1. 
    ```console
    npx create-nuxt-app <project-name>
    ```
2. préparation de l'auth: https://auth.nuxtjs.org/guide/setup/
    ```console
    npm install --save-exact @nuxtjs/auth-next
    npm install @nuxtjs/axios #lancez ceci si on n'as pas encore installé axios durant l'installation de nuxt
    ```
3. configuration
    ```javascript nuxt.config.js
    const api_base_url = <url>
    {
        modules: [
            '@nuxtjs/axios',
            '@nuxtjs/auth-next'
        ],
        auth: {
            strategies: {
                laravelSanctum: {
                    provider: "laravel/sanctum",
                        url: api_base_url,
                        endpoints: {
                        login: {
                            url: "/api/login",
                        },
                    },
                },
            },
        },
        axios: {
            // Workaround to avoid enforcing hard-coded localhost:3000: https://github.com/nuxt-community/axios-module/issues/308
            baseURL: api_base_url + "/api",
            proxy: true,
            credentials: true,
        },
        proxy: {
            "/laravel": {
            target: "https://laravel-auth.nuxtjs.app",
            pathRewrite: { "^/laravel": "/" },
            },
        },
    }

    ```
 4. Login