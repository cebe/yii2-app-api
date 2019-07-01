# yii2-app-api

> OpenAPI Spec to API in 3, 2, 1... done!

Yii Framework Application Template for quickly building API-first applications.

Based on [yii2-openapi](https://github.com/cebe/yii2-openapi) (code generator) and [php-openapi](https://github.com/cebe/php-openapi) (specification reader and validator).

[![Latest Stable Version](https://poser.pugx.org/cebe/yii2-app-api/v/stable)](https://packagist.org/packages/cebe/yii2-app-api)
[![Total Downloads](https://poser.pugx.org/cebe/yii2-app-api/downloads)](https://packagist.org/packages/cebe/yii2-app-api)
[![License](https://poser.pugx.org/cebe/yii2-app-api/license)](https://packagist.org/packages/cebe/yii2-app-api)


## Demo

[![asciicast](https://asciinema.org/a/GSnZFeL0beAwLvbhIn50oVI9w.svg)](https://asciinema.org/a/GSnZFeL0beAwLvbhIn50oVI9w)

## Overview

This application template consists of 3 application tiers:

- `api`, contains the Yii application for the REST API.
- `console`, contains the Yii application for console commands, cronjobs or queues.
- `backend`, contains the Yii application for a CRUD backend on the API data.


## Setup

    composer create-project cebe/yii2-app-api my-api
    cd my-api
    cp env.php.dist env.php

## Generate Code

### Console

Run `./yii gii/api` to generate your API code. The `--openApiPath` parameter specifies the path to your OpenAPI
spec file. The following example will generate API code for the [OpenAPI petstore example](https://github.com/OAI/OpenAPI-Specification/blob/3.0.2/examples/v3.0/petstore-expanded.yaml).

    ./yii gii/api --openApiPath=https://raw.githubusercontent.com/OAI/OpenAPI-Specification/3.0.2/examples/v3.0/petstore-expanded.yaml

Run `./yii gii/api --help` for a list of configuration options. You may also adjust the configuration in `config/gii-generators.php`.

Then set up the database:

    ./yii migrate/up
    ./yii faker

### Web

To use the web generator, start the backend server:

    cd backend
    make start

open `http://localhost:8338/gii` and select the `REST API Generator`.

![Gii - REST API Generator](docs/img/gii-generator.png)

Enter the path or URL to the "OpenAPI 3 Spec file", e.g. `https://raw.githubusercontent.com/OAI/OpenAPI-Specification/3.0.2/examples/v3.0/petstore-expanded.yaml`.

Click "Preview":

![Gii - REST API Generator - Generated files](docs/img/gii-generator-files.png)

Click "Generate" to generate API files.

Then set up the database by running the following commands on the command line:

    ./yii migrate/up
    ./yii faker

## Try it

    cd api
    make start

Your API is now available at `http://localhost:8337/`. Try to access an endpoint of your spec via `curl`:

    $ curl http://localhost:8337/pets
    [
        {
            "name": "Eos rerum modi et quaerat voluptatibus.",
            "tag": "Totam in commodi in est nisi nihil aut et."
        },
        {
            "name": "Voluptas quia eos nisi deleniti itaque aspernatur aspernatur.",
            "tag": "Temporibus id culpa dolorem sequi aut."
        },
        {
            "name": "Facere aut similique laboriosam omnis perferendis et.",
            "tag": "Quo harum quo et ea distinctio non quam."
        },
        ...
    ]

## Application structure

- `api/` - API application tier
  - `config/` - configuration for API tier
    - `url-rules.php` - custom URL rules
    - `url-rules.rest.php` - URL rules **generated** from OpenAPI Description
    - `components.php` - application components
    - `app.php` - Yii application config (+ overrides for different environments `app-*.php`)
  - `controllers/` - Controller classes **generated** from OpenAPI Description
  - `web/` - public web directory for API application

- `backend/` - Backend application tier
  - `config/` - configuration for Backend tier
    - `components.php` - application components
    - `app.php` - Yii application config (+ overrides for different environments `app-*.php`)
  - `controllers/` - Controller classes
  - `views/` - View files
  - `web/` - public web directory for Backend application

- `common/` - common code files
  - `models/` - model classes **generated** from OpenAPI Description
  - `migrations/` - database migrations **generated** from OpenAPI Description

- `config/` - Common configuration for all application tiers
  - `components.php` - Yii application components (+ overrides for different environments `components-*.php`)
  - `env.php` - Environment setup (YII_DEBUG, YII_ENV, path aliases, composer autoloader)
  - `events.php` - Class wide event listeners
  - `gii-generators.php` - configuration for the Gii code generator (allows to set default values for the ApiGenerator)
  - `params.php` - Configuration for `Yii::$app->params`

- `console/` - Console application tier
  - `config/` - configuration for Console tier
    - `components.php` - application components
    - `app.php` - Yii application config (+ overrides for different environments `app-*.php`)

- `logs/` - log files
- `runtime/` - temporary runtime files

# Support

**Need help with your API project?**

Professional support, consulting as well as software development services are available:

https://www.cebe.cc/en/contact

Development of this library is sponsored by [cebe.:cloud: "Your Professional Deployment Platform"](https://cebe.cloud).
